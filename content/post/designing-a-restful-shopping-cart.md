---
title: "Designing a RESTful shopping cart"
date: "2018-03-10"
tags: [rest, api-design]
image: img/posts/shopping_cart.jpg
---

Designing APIs for inter microservice communication is one of the most difficult aspects of modern software engineering and the reasons range in a very broad spectrum. First of all, microservices is a relatively new *trend* and virtually everyone in the software engineering community talks about them nowadays. However, I believe that we still don't know what exactly they are (let alone how they will develop in the future) and therefore, we can't always design them in an efficient way. We've all experienced microservices that weren't so "micro" after all (how "micro" they should be anyway?).

Adding to it, REST is a marvelous architecture (developed back in 2000 by Roy Fielding as part of his [doctoral dissertation](https://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm)). However, it is as misunderstood as beautiful. The web is packed of "RESTful" web services which are not so RESTful after all. The requirement to communicate with such a system can create previously unseen obstacles, making design very challenging. Furthermore, more often than not, the ecosystem in which a microservice is being developed, contains legacy system(s), which impose very difficult constraints to the design, usually leading to exceptions and inconsistencies, which usually lead to problems further down the road.

Among others, the above mentioned phenomena, can increase the degree of difficulty of designing a RESTful API for inter microservice communication. In this post, I will endeavor to share my journey and outcome of designing such an API.

# The case study

This example attempts to design an efficient, RESTful API as a solution to the problem of creating a microservice that is responsible for handling the lifecycle of a shopping cart.

## Assumptions

### Authentication - Authorization

Throughout this example we consider authentication - authorization functionality to exist and to be provided by a separate microservice. Therefore, a JWT token (or some other token) is supposedly provided by this microservice and included in the `Authorization` header in all HTTP requests. In addition, we assume that authorization is not required for the HTTP request to list all available products.

### Requests - Responses body

The body (as well as the headers) provided in the following HTTP requests and responses is an example which attempts to meaningfully demonstrate the essence of the argument and by no means are complete or fully functional. For instance, in the *list all products* response, products are obviously not represented merely by their IDs and prices, but believing that this structure suffices to communicate the essence of the call, they are intentionally left partially complete.

### API Design decisions

Throughout this post, **API design** is on the spotlight. Neither *application design*, nor *technological decisions* (e.g. persistence layer technology) will not be covered since they do not constitute part of the *API design*.

## Making some decisions

### Which calls

Identifying the correct HTTP calls can be trickier than it actually sounds. My advice would be to approach the problem by carefully producing sequence diagrams to cover all the use cases of the new system. Given that we have them, we can proceed to identify the interaction the system will have with the rest of the systems and therefore define the endpoints and HTTP calls that cover these.

### Persisting data

A common misconception concerning REST is that one is not allowed to store any data in order to implement a RESTful web service. This is not quite true. Persisting data is perfectly fine as long as these data do not concern the *state* of the client. So, persisting the cart data will not make you uncompliant with REST. In essence, what the architecture is trying to achieve is to make each request *independent of any sort of state*. There lies a fundamental REST aspect: **statelessness**. So, by all means, we go ahead and persist the cart data in our system.

### Eager or lazy initialization

An interesting decision we have to make is *when* to initialize the sopping cart. There are two options: we either *lazily* create the cart the first time we're asked to put a product in it or we *eagerly* create it with a separate call before we can put any products in it. In the first case, we use one less call, which sounds like a good thing and we do not create a shopping cart for a user that will never put anything in it. However, a small ambiguity is introduced in our *put a product in the cart* call, since it will return `201 CREATED` the first time it is called (as it will also create a resource - the shopping cart) and `200 OK` for any subsequent call (since the shopping cart already exists and we're just putting products in it). Although the first two pros seem quite strong, the final decision is to go with the latter approach for clarity reasons.

### POST without body

Often we face a situation in which we wish to either create a resource or trigger an action, but there are no data to be submitted to the system. We might get tempted to use a `GET` request, since the request will not have any body. However, we should not succumb to it. Using a `POST` HTTP request (or a `PUT` one, depending on the situation) without a body for these purposes is perfectly fine. Beware though that, in such cases, it is important to remember to include the `Content-Length` header with value `0`, since its absence may cause problems to proxies. This is demonstrated both in the request to create a shopping cart and in the one that triggers the checkout.

## HTTP methods

### List all products

A `GET` HTTP request is sent to retrieve all the available products. A list of all available products is returned.

#### Request

```
GET /products
Content-type: application/json
Accept: application/json
```

#### Response

```
200 OK
Content-type: application/json
```

```
{
  "products": [
    {
      "id": 298743,
      "price": {
        "total": 23,
        "tax": 6,
        "currency": EUR
      }
    },
    {
      "id": 287543,
      "price": {
        "total": 14,
        "tax": 3,
        "currency": EUR
      }
    }
  ]
}
```

### Create a shopping cart

A `POST` HTTP request is sent. A shopping cart is created. The `Location` header is used to link to the newly created resource (the cart) in order for the client to be able to access it without querying anew.

#### Request

```
POST /cart
Authorization: Bearer eyJhbGciOiNIUzI1JiIXVCJ9...TJVA95OrM7E20RMHrZDcEfxjoIZgeFONFh7HgQ
Content-type: application/json
Accept: application/json
Content-Length: 0
```

#### Response

```
201 Created
Content-type: application/json
Location: /cart/{cart_id}
```

### Put a product in the cart

A `POST` HTTP request is used to put a product in the cart. The product is sent as part of the request body. The reply contains all cart data in order not to force the client to query again for it.

#### Request

```
POST /cart/{cart_id}
Authorization: Bearer eyJhbGciOiNIUzI1JiIXVCJ9...TJVA95OrM7E20RMHrZDcEfxjoIZgeFONFh7HgQ
Content-type: application/json
Accept: application/json
```

#### Response

```
200 OK
Content-type: application/json
```

```
{
  "cart_id": 174826,
  "products": [
    {
      "id": 298743,
      "quantity": 1
    },
    {
      "id": 287543,
      "quantity": 1
    }
  ],
  "payment": {
    "total": 74,
    "tax": 17,
    "currency": EUR
  }
}
```

### Get cart contents

A `GET` HTTP request is used to fetch the contents of a shopping cart.

#### Request

```
GET /cart/{cart_id}
Authorization: Bearer eyJhbGciOiNIUzI1JiIXVCJ9...TJVA95OrM7E20RMHrZDcEfxjoIZgeFONFh7HgQ
Content-type: application/json
Accept: application/json
```

#### Response

```
200 OK
Content-type: application/json
```

```
{
  "cart_id": 174826,
  "products": [
    {
      "id": 298743,
      "quantity": 1
    },
    {
      "id": 287543,
      "quantity": 1
    }
  ],
  "payment": {
    "total": 74,
    "tax": 17,
    "currency": EUR
  }
}
```

### Checkout

A `POST` HTTP request will trigger the checkout action, buying all products currently withing this cart.

#### Request

```
POST /cart/{cart_id}/checkout
Authorization: Bearer eyJhbGciOiNIUzI1JiIXVCJ9...TJVA95OrM7E20RMHrZDcEfxjoIZgeFONFh7HgQ
Content-type: application/json
Accept: application/json
Content-Length: 0
```

#### Response

```
200 OK
Content-type: application/json
```

# Conclusion

Designing RESTful APIs is often misunderstood or poorly performed. However, REST is truly a gift, leveraging our systems architecture and using it right can prove gold for our microservices. As usually, there is not a single approach to the problem of designing a RESTful API, but it is worthwhile to think carefully of our decisions, challenge them and try hard to be compliant with the essence of this architecture. The benefits can be of immense value.
