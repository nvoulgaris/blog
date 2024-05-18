+++
title = "GraphQL introduction"
date = "2024-05-18"
image = "img/posts/graphql_introduction.jpg"
tags = ["GraphQL"]
description = "Simplifying data fetching for modern applications"
+++

Over the past few years, REST has evolved into the predominant choice when building web applications. Powerful as it is, it still has weaknesses, and despite it can usually get the job done, it might not be the best tool for every job.

GraphQL has gained a lot of ground lately, mainly because it can thrive in problems where REST falls short. The reason is that the mindset when working with GraphQL is completely different, essentially constituting a paradigm shift.

In this article, we will go over the key concepts of GraphQL.

## What is GraphQL
Graph Query Language (GraphQL) is a [specification](https://spec.graphql.org) for a declarative query language, which provides access to a mesh of interconnected data. Essentially, it is a way to give access to a dataset, which can be traversed as the client wishes.

### Schema
A strongly typed schema is used to model the data and the client can use it to query anything defined in it. Below is a simplistic example, which both illustrates what a schema looks like and will also serve as the basis of the examples in this article.

```graphql
type Author {
  id: ID!
  name: String!
  books: [Book!]!
}

type Book {
  id: ID!
  title: String!
  publishedYear: Int!
  author: Author!
}

type Query {
  books: [Book!]!
  book(id: ID!): Book
  authors: [Author!]!
  author(id: ID!): Author
}

type Mutation {
  createBook(title: String!, authorId: ID!, publishedYear: Int): Book!
  createAuthor(name: String!): Author!
}

schema {
  query: Query
  mutation: Mutation
}
```

The schema defines the following categories:
* **types**: Representations of resources. These constitute the nodes of the graph, while the edges are defined by the relationships between them. In this case, an edge would connect the `Author` nodes to the `Book` nodes that they have written.
* **queries**: These can be used by the client to fetch data from the graph.
* **mutations**: These can be used by the client to alter the state of the graph.

## Key features
Thinking in terms of GraphQL is a whole new world. It requires a mentality shift

### Declarative data fetching
GraphQL queries are *declarative*. This means that the client defines the data that are returned. For instance, given the aforementioned books schema, a client may wish to fetch just the ID and title of the books, using the following query:

```graphql
query {
  books {
    id
    title
  }
}
```

However, they could also choose to include the publish year as part of the same query, as follows.

```graphql
query {
  books {
    id
    title
    publishedYear
  }
}
```

### Hierarchical
The *declarative* property becomes much more powerful when combined with the *hierarchical* property. The hierarchical structure reflects the nested relationships of data, making it intuitive to request related data in a single query, as this structure is also mirrored in the JSON response.

Building on the previous query, the client may also wish to get some data on the author of each book as part of the same query. This can be done as follows:

```graphql
query {
  books {
    id
    title
    publishedYear
    author {
      id
      name
    }
  }
}
```

It has to be noted that GraphQL does not specify anything regarding data storage. It only specifies the way in which the client may fetch the data. This means that the authors may be stored in a different database, be part of a configuration, or even be stored in a completely different service. The client can still fetch the two pieces of information with a single query, regardless of their storage details.

### Strongly typed
The contract between the server and the client is strongly typed. This is achieved by the schema definition, which describes the types of data available and the relationships between them. Apart from letting the client know what data is available, this also allows the server to validate a query before processing it.

### Self-documenting
GraphQL addresses the documentation pain point in a very elegant way. Its *introspection* feature allows clients to query the schema itself, essentially providing live, executable and always up-to-date self-documentation.

## GraphQL vs REST
In the introduction, I mentioned that GraphQL can thrive in problems where REST is weak (and vice versa).

### Data fetching
* GraphQL: A single endpoint is exposed (typically `/graphql`), which gives access to the available queries and mutations. The client drives the request, defining the fields that will be returned. This is an extremely powerful feature, as a client can fetch multiple resources by issuing a single network request (HTTP is typical, but not mandatory). This reduces the chances of over-fetching or under-fetching and can be a critical advantage in demanding environments, such as mobile applications, in which battery life and data consumption are important.

* REST: A RESTful API typically consists of multiple endpoints, the response of which is predefined. Therefore, clients may be forced to issue multiple requests to get the data they need.

### Schema and validation
* GraphQL: A strongly typed schema is defined in the server. Clients can introspect it to understand and use the contract. By definition, incoming requests are validated and only processed when they are valid.

* REST: A schema is only implicitly defined and not communicated to the client. Therefore, the client might issue invalid requests. Incoming requests need to be processed by the server to judge their validity.

### Versioning
* GraphQL: Versioning is not defined. Adding fields is not a breaking change, but this can become a serious problem in case a breaking change needs to take place. Despite the fact that there are workarounds, obstacles can emerge because of the absence of a versioning mechanism.

* REST: Although there is not an officially defined versioning mechanism, implementing versioning in a RESTful API is trivial and can be achieved in numerous ways. The most typical one is to include a version part in the URL, such as `/api/v1/books`.

### Error handling
* GraphQL: GraphQL does not use the HTTP status codes, as it is not mandatory to be server over HTTP anyway. Typically, a response to a GraphQL endpoint will resolve with a `200` HTTP status code.  An `errors` field is included in the response, which can provide detailed information about what went wrong.

* REST: Extensive use of the HTTP status codes allows the client to easily identify the outcome of the request.

### Caching
* GraphQL: Caching can be a challenge when working with GraphQL. The specification does not provide a designated solution. Additionally, the queries are driven by the clients, which means that each query can be different, making caching quite a difficult problem to solve.

* REST: The REST architectural constraints specify that "responses indicate their own cacheability". The built-in HTTP caching mechanisms can be leveraged to implement caching in a RESTful API.

### Documentation
* GraphQL: GraphQL is self-documented, because of the enforced, strongly typed schema. Additionally, the clients can take advantage of its introspection feature to understand the schema.

* REST: Documentation is not enforced by the architecture. There are plenty of solutions to provide documentation for a RESTful API, such as Swagger, but all of them need to be maintained independently and can be left out-of-date.

## Conclusion
