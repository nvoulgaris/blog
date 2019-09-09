---
title: "Software design with lambda expressions"
date: "2019-09-01"
tags: [software design,functional programming]
image: img/posts/software_design_with_lambda_expressions.jpg
---

Lambda expressions are powerful and allow us to write concise, elegant, declarative code. A lot of people has already adopted them, mainly leveraging the power of streams in iterations, but lambda's toolkit is far richer than that. This is why I decided to write this blog post and explore some aspects of how lambda expressions can prove useful in software design.

We will do this exploration via a real world case study in order to demonstrate how we can apply these principles in our everyday work.

# The case study

Instead of creating a new case study, from scratch, I decided to extend the one from my previous blog [post](https://nvoulgaris.com/open-closed-principle-a-case-study), in which we examined closely the problem of input validation. We assumed an android application that displays a form and we came up with a robust solution to validate the input of this form (leaving out android specifics on purpose and simplifying a bit to put emphasis on the right parts).

The key takeaway was that after drafting a first, working version of the code, we refactored our way to a much better crafted one. We applied the Open-Closed Principle so that we could extend the behavior of our validation module (e.g. add validation for new fields, such as a postcode field) without having to modify our existing validation code. In this way, we improved the design of our solution by making the code *less fragile* and therefore *more maintainable*.

## Room for improvement

However, in software, there is no such thing as a *perfect* design and there never will be. There will always be things to improve. As responsible, professional software craftspeople, we should always study the pros and cons of our solutions and know their weaknesses and limitations and, as I always like to say, *work the trade-offs*.

Considering the solution of the previous post, there is definitely room for improvement. First of all, as already mentioned in that post, we should apply the Dependency Inversion Principle to invert the dependencies between the `ValidationService` and `EmailValidator` and `PhoneValidator` (currently there is a transitive dependency between them, while the former should not know about the latter). A second point of interest is the life cycle of the `ViewValidator` object that we create. Please remember that we designed it to be used like this:

```
formViews.forEach(view -> {
    ViewValidator validator = ViewValidatorFactory.makeFor(view);
    validator.validate(view.getText());
});
```

*Allow me to refresh our memory on a few basic points for this case study. We assumed that we have a list of `View` objects (in android all UI elements derive from `View`) and that all these objects have a tag, which we can retrieve using a `getter`, denoting the view’s input type (e.g. `Email` or `Phone`) and a `getter` to retrieve the text of the view.*

In this case we create a new instance of `ViewValidator` for every view that we wish to validate. However, this does not come naturally from the design of the class. *We do not know it*. We simply *assumed* it. And these kind of assumptions can lead to a great deal of problems down the road. What if we have a bunch of similar views to validate (e.g. 3 e-mail fields)? Should we use the same instance for all 3 of them or is this instance disposable and we should create a fresh one for each validation? Well, the answer is that there is no way to know (unless, of course, we open the `ViewValidator` source code and have a look ourselves). *The design of the class does not communicate its intent* as far as the life cycle of the object is concerned.

This is clearly an issue that could - and perhaps should - be addressed. Thinking carefully about the architecture of the system (its design on a macro level) is essential, but taking the time to think through our micro level design (e.g. class design) is equally important.

# The loan pattern

Thankfully, there is a design pattern, which solves exactly this problem, in a *very elegant way* and its name is the **loan pattern**. I first came across it while reading Venkat Subramaniam's excellent book [Functional Programming in Java](https://www.goodreads.com/book/show/17698629-functional-programming-in-java). Venkat does a wonderful job explaining this pattern as it naturally emerges while refactoring a real world piece of code and I suggest that you read it (see section *"Creating Fluent Interfaces Using Lambda Expressions"*), but I will try to explain the basic points myself here.

Essentially, the pattern removes the responsibility of dealing with the object's life cycle from the function that uses it. Instead, this responsibility lies with the class itself. In order to achieve this, we *create* a resource and *pass* it to the function. As soon as the function terminates, the resource is *destroyed*.

In our case, to achieve this, we would ideally want to write something like this (remember that `tags` is what will be used to determine the type of validation that should be applied and `value` is the value that is to be validated)

```
Validator.validate(
  validator -> validator.withTags("email").withValue("someone@example.com")
);
```

The point is that whoever uses this piece of code does not have to worry about the life cycle of the `Validator` object. An instance will be passed as an argument and destroyed as soon as the `validate()` function terminates. This is where the name comes from. The `Validator` object is *loaned* to the function.

This is an incredibly *smart* and *elegant* solution to a very sneaky problem. Lambda expressions empower us to implement it. Let's dive into the implementation.

# Applying the loan pattern

Assuming that the `Validator` class is to be used as stated above, the obvious challenge would be to come up with a way to make use of the loaned resource in the `validate()` function. This can be easily achieved with the `Consumer` functional interface (`java.util.function.Consumer`), which is designed to accept an object and execute a piece of code on it. So, redesigning our `Validator` class like the following, would do the job.

```
public class Validator {

    private static String COMMA = ",";

    private String tags;
    private String value;

    private Validator() {
    }

    public Validator withTags(final String tags) {
        this.tags = tags;
        return this;
    }

    public Validator withValue(final String value) {
        this.value = value;
        return this;
    }

    public static List<Violation> validate(final Consumer<Validator> block) {
        final Validator validator = new Validator();
        block.accept(validator);
        return validator.applyValidations();
    }

    private List<Violation> applyValidations() {
        return Arrays.stream(tags.split(COMMA))
                .map(this::validationFor)
                .map(validation -> validation.applyTo(value))
                .flatMap(List::stream)
                .collect(Collectors.toList());
    }

    private Validation validationFor(final String tag) {
        switch (tag) {
            case "Email":
                return new EmailValidation();
            case "Phone":
                return new PhoneValidation();
            default:
                return new DefaultValidation();
        }
    }
}
```

There's a lot of things to notice in this class, so let's take them one by one.

* First, the `validate()` function, does exactly what we discussed earlier. It accepts a piece of code meant to be executed in an instance of `Validator`. It creates this instance and executes this piece of code on it. This serves in "configuring" the object with the right tags and value. Then, it applies the appropriate validations. Notice that we also made the constructor private, essentially *disallowing direct instantiation* and explicitly *removing the burden of this responsibility from the caller*. We make sure that no one will instantiate this class (other than the `validate()` function of course). The `withTags()` and `withValue()` functions act as builder functions that allow us to chain our calls.

* Secondly, instead of an explicit factory class to create specific `Validation` objects based on the tags, we achieve this in the `validationFor()` factory method. This has the extra benefit of encapsulating the `Validation` polymorphic instantiation logic in the `Validator` class, which is the only one that needs to know about it anyway. The various `Validation` derivatives (`EmailValidation`, `PhoneValidation` etc) are implementation details and are subject to change at any time. No one should depend on them.

* Finally, the `applyValidations()` function pretty much does what the client in the previous version was doing. It splits the tags of the view and creates an appropriate `Validation` for each tag. Then it applies this validation to the value and finally, it flattens all the violations in a single list to return it. Usage of lambda expressions makes this function declarative, elegant and very readable.

Below is the `Validation` interface

```
public interface Validation {

    List<Violation> applyTo(final String value);
}
```

and its three derivatives

```
public class EmailValidation implements Validation {

    @Override
    public List<Violation> applyTo(final String value) {
        // Actual email validation code omitted for brevity
        return Arrays.asList();
    }
}

public class PhoneValidation implements Validation {

    @Override
    public List<Violation> applyTo(final String value) {
        // Actual phone validation code omitted for brevity
        return Arrays.asList();
    }
}

public class DefaultValidation implements Validation {

    @Override
    public List<Violation> applyTo(final String value) {
        return Arrays.asList();
    }
}
```

That's it. We have implemented the loan pattern.

# Retrospective

So, by this point you might be wondering if it is worthwhile to go through all this refactoring. Let's take a step back and examine what we have achieved.

* First of all, the we still comply to the Open-Closed principle and therefore *we can extend the module's behavior without modifying existing code*.

* Additionally, the *responsibility of the life cycle* of the `Validator` object *does not lie with the caller*, but we have already taken care of it.

* Furthermore, what's really important - and unfortunately seriously underestimated - is that *the design communicates this decision*.

* Finally, an additional advantage is that `Validation` instantiation logic is *encapsulated* in the `Validator` class, along with the rest of its implementation details.

As far as the form validation case study is concerned, it might worth it or it might not. To be honest, it doesn't matter. I did take the trouble to do exactly this refactor (except in Kotlin) the first time that I had to enhance our validation feature after having read Venkat's book, but that is up to each one of us. Once again, as software craftspeople it's us that should work the trade-offs everyday and make the call. In any case, the key point is that *we can use functional interfaces and lambda expressions to produce elegant and robust software designs*.

# Conclusion

Lambda expressions allow us to write concise and declarative code, but they offer way more than that. They can be used as a *design tool*. High order functions (functions that take functions as arguments) are a game changer and they can fundamentally alter our perceptions on architecture, design patterns and software design.

Refactoring to transfer the responsibility of managing a resource' s life cycle from the caller to the callee may be worthwhile or not, depending on the problem in hand. It is important knowing that we have the option and being able to make a call on a per case basis.
