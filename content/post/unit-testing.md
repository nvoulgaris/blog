---
title: "Unit testing best practices"
date: "2018-01-30"
tags: [unit-testing]
image: img/posts/test_board.jpg
---

As part of the onboarding process of every new developer in [Tripsta](http://www.tripsta.com/), I am required to deliver a training on unit testing basics. I would like to share the most valuable techniques, methodologies and best practices that I have collected over the years. I believe that they constitute the pillars of a sold foundation that every developer should have.

Allow me to start unconventionally (the way I love it), and before talking about what tests *are*, stating firmly what tests **are not**.

> Tests are not nice to haven

> Tests are not negotiable

When I hear phrases like *"If we have time, we'll write some tests too"* or *"It costs 13 story points, but since there is no time, we can  make it 8 if we don't write tests"* I want to...
Tests should be an integral part of writing software.

# Best practices

## Naming

Some people are bad at naming. Some other (such as me) are terrible at it. In any case, taking the time to come up with a proper name for everything in our code *is worth it*. Regardless of how much time we need. Uncle Bob (Robert Martin) likes to say *"with code, we do more reading than writing, by a huge factor. Which of those operations should be made efficient?"* Naming **matters**!!

> Write the tests you'd want to read

Before stop writing a test and moving to the production code, ask yourself these two questions:

 * Does the test clearly express its behavior?
 * Is it easy to understand?

Usually, a developer that struggles to come up with a proper name will settle for a mediocre one, that does not express behavior properly, or even a bad one, which is hard to understand and misleads its reader.

> Tests should be a documentation of the module's behavior?

Whenever we come across a piece of code that we did not write, we want to be able to read its test suite and figure out what this code does. So, take the time (however much you need) to name your tests (and the variables and functions in them) as best as you can and when you come across a mediocre or a bad name, *change it to something better* (leaving the code better than you found it, as Uncle Bob would say).

## Isolation

This whole point can be summarized in the following sentence:

> Tests should leave the system in the state that they found it

The last thing that we would like to face is a failing test, causing the following 5 tests in the suite to fail too. Whenever a test is failing, it should clearly declare an aspect of the software that is not functioning properly and point us to it immediately.

## Watch the test fail

When should we stop writing the test and start writing the production code? That is a surprisingly hard to answer question for a lot of people when I give the training. Take a minute and think about it before reading further. There are a couple of questions I like asking myself before I stop writing the test.

 * **Does it fail for the right reason?** What good is a test if it does not break when the functionality breaks? How can we know that this won't happen if we do not watch the test fail and make sure that it fails for the *right reason*?
 * **Are the diagnostics clear?** There will come a time in the future that this test will break and then someone (most probably us) will have to understand what is wrong and fix it. How hard will it be to fix it if we cannot tell what is wrong? A few months ago, I fell into exactly this pitfall, a test that I had written (quite a few months back) failed against the production code that I had written and all I had in the console was:

```
Expected: 1
Got: 0
```

I forced myself in a debugging session to figure out what was wrong. If only I had taken the time to make the diagnostics clear enough...

## Triple A rule

## Single assertion

How many assertions should a test have? The answer should always be *one*. What message is a red bar sending to us? That something is wrong in the system. Which is our reflex move? To find out what is this. This is exactly why we want our tests to be shouting out loud the reason for their failure. If a test fails, we should know, just by reading its name, what the problem is. How can this happen if a test fails for multiple reasons though?

> Unit tests should fail for one and only one reason

Watch out for a common misconception though. The following test, contains two assertions. Does it violate the single assertion rule?

```
@Test public void
calculatorShouldGeneratePositiveEvenIntegers() {
  int number = calculator.generate();

  assertThat(number > 0).isTrue();
  assertThat(number % 2).isEqualTo(0);
}
```

There may be two *physical* assertions, but they essentially constitute a single *logical* assertion. This test will fail *if and only if the calculator does not generate positive even numbers*, as opposed to the following test:

```
@Test public void
calculatorShouldDivideNumbers() {
  int number = calculator.divide(2, 2);
  assertThat(number).isEqualTo(1);

  Executable divideByZero = () -> calculator.divide(4, 0);
  assertThrows(ArithmeticException.class, divideByZero);
}
```

This test will both when calculator fails to divide correctly and when the error case of dividing by zero does not throw an `ArithmeticException`. Therefore, in essence, we want to avoid a series of *act-assert* sequences. A single act followed by more than one physical assertions is fine.

## Assert first

*Assert first* is a technique described in Kent Beck's excellent book [Test Driven Development: By Example](https://www.goodreads.com/book/show/387190.Test_Driven_Development). As counterintuitive as it may sound (and feel for someone not used to it), it comes with tons of advantages and it will become second nature given some time. The main idea lies in the fact that writing a test presents multiple problems. The two principal ones are *"what is the right answer?"* and *"how am I going to check"*. Taking this bottom up approach helps us focus on the target and avoid overengineering the test.

Assuming that I have a business requirement that a booking without booking ID is invalid, and I am writing the booking validator logic, I may start as follows:

```
@Test public void
validatorShouldThrowInvalidBookingExceptionWhenBookingIdIsNull() {
  assertThrows(InvalidBookingException.class, validateBooking);
}
```

Starting off with the *assert*, I know both the right answer and how to check it. I am also driven to the proper act for my assertion.

```
@Test public void
validatorShouldThrowInvalidBookingExceptionWhenBookingIdIsNull() {
  Executable validateBooking = () -> validator.validate(booking);

  assertThrows(InvalidBookingException.class, validateBooking);
}
```

Now there is only one step missing, the arrange part. I need a booking and it should have a `null` booking ID.

```
@Test public void
validatorShouldThrowInvalidBookingExceptionWhenBookingIdIsNull() {
  Booking booking = BookingBuilder.aBooking().withBookingId(null).build();

  Executable validateBooking = () -> validator.validate(booking);

  assertThrows(InvalidBookingException.class, validateBooking);
}
```

# Conclusion

Tests are an integral part of the system. They should be designed and maintained. We should care for them and we should take the time to write the *right tests* and in the *right way*.

*P.S. I would also love to cover the whole "test state vs test behavior" topic, but this post is already lengthy enough and this is a really long topic*
