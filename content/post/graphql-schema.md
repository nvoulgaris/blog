+++
title = "The Anatomy of a GraphQL Schema"
date = "2024-07-14"
image = "img/posts/graphql_schema.jpeg"
tags = ["GraphQL"]
description = "The Blueprint for Graph Data access"
+++

One of the key features of GraphQL is that it is client-driven. The server provides access to a mesh of interconnected data and the client can navigate in it. The contract between the two parties, which defines the protocol for this data exchange, is a GraphQL schema.

The GraphQL schema mechanism possesses some clever and powerful features, in order to support this elaborate communication. In this post, we will explore both the basic and a few advanced features.

## Types

### Objects
The objects represent the nodes of the graph. They are the primary building blocks of a GraphQL schema, as they define the structure of the data. An object definition also contains the fields of the object. The `type` keyword is used to define an object.

The following schema snippet defines an object that represents a book entity.

```graphql
type Book {
  id: ID!
  title: String!
  publishedYear: Int!
}
```

### Scalars
Scalar types are the primitive data types in GraphQL, and they are used to define the type of fields. GraphQL supports the following:

 * `String`
 * `Int`
 * `Float`
 * `Boolean`
 * `ID`

While these may cover the needs of a basic schema, it is easy to see that they don't suffice for more advanced use cases. For instance, there is no support for dates. However, this is easily solved, as GraphQL allows the definition of custom scalars. Regarding the schema, creating a custom scalar is as easy as defining it, using the keyword `scalar`.

```graphql
scalar Date
```

Additional work is required in the application code though, to define how it should be serialized/deserialized etc.

### Enums
Enums are inherently supported in GraphQL schema, just by using the `enum` keyword.

As an example, let's define an enum to describe the type of a physical book.

```graphql
enum BookType {
  PAPERBACK
  HARDCOVER
}
```

### Lists and Non-Null
While objects, scalars and enums are the only kinds of types that can be defined in a GraphQL schema, there are also a few type modifiers that can be used with them.

Nullability is explicitly declared, by the absence of the Non-Null, `!` modifier. So, `title: String` permits null values, whereas `title: String!` disallows them.

The list modifier `[]` declares an array of the given types. So, for example, `books: [Book!]!` refer to a non-null list of non-null books.

## Relationships

As already explained, the objects represent the nodes of the graph. In addition to that, an object may refer to another object. These relationships define the edges of the graph and they may be either bidirectional or unidirectional.

In the following example, types `Book` and `Author` are connected via a bidirectional relationship.

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
```

To make this relationship unidirectional, either the `books` field could be removed from the `Author` type or the `author` field could be removed from the `Book` type.

## Root types

The root types are the entry points to the schema for the client. These (and only these) can be used to access the graph data. Read and write access points are segregated, making clear the intention behind each access point.

### Query

The `Query` type defines read-only operations. 

```graphql
type Query {
  books: [Book!]!
  book(id: ID!): Book
  authors: [Author!]!
  author(id: ID!): Author
}
```

An example query would look as follows.

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

### Mutation

The `Mutation` type is used to define operations that result in state modifications.

```graphql
type Mutation {
  createBook(title: String!, authorId: ID!, publishedYear: Int): Book!
  createAuthor(name: String!): Author!
}
```

The `createBook` mutation could be used like that.

```graphql
mutation {
  createBook(title: "GraphQL for Experts", authorId: "A1", publishedYear: 2024) {
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

### Subscription

The third and last root type is the `Subscription` type, which is used to provide access to real-time updates on a specific type.

```graphql
type Subscription {
  bookCreated: Book!
}
```

Using the subscription would look as follows.

```graphql
subscription {
  bookCreated {
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

## Arguments

Arguments are inputs provided to fields within queries, mutations, or subscriptions to specify or filter/sort the data being requested or to perform actions with certain parameters.

Assuming we wanted to provide a way for the client to filter the publications based on certain criteria, we could define the following arguments.

```graphql
type Query {
  publications(keyword: String, publishedYear: Int, type: String): [Publication!]!
}
```

## Input types

Input types are passed as arguments to mutations. They have to be defined individually. The `input` keyword is used to define them.

For instance, if we wanted to avoid passing 3 separate arguments to the `createBook` mutation, we could define a `BookInput` instead.

```graphql
type Mutation {
  createBook(input: BookInput!): Book!
}

input BookInput {
  title: String!
  authorId: ID!
  publishedYear: Int
}
```

Input types resemble objects a lot. However, even if they are identical, their use is not interchangeable. An object cannot be passed as an argument to a mutation and an input cannot be defined as the return type of a query.

## Interfaces and Unions

Interfaces, similar to many Object-Oriented programming languages that support them, are abstract types that other types can implement.

They are powerful for creating abstractions in a GraphQL schema. For instance, below we enrich the `Book` type by creating the `Publication` abstraction as well as two more derivatives of it; `Magazine` and `Newspaper`.

```graphql
interface Publication {
  id: ID!
  title: String!
  publishedYear: Int!
}

type Book implements Publication {
  id: ID!
  title: String!
  publishedYear: Int!
  author: Author!
}

type Magazine implements Publication {
  id: ID!
  title: String!
  publishedYear: Int!
  issueNumber: Int!
}

type Newspaper implements Publication {
  id: ID!
  title: String!
  publishedYear: Int!
  date: String!
}

type Query {
  publications: [Publication!]!
}
```

What might seem as counter-intuitive, with respect to interfaces in some programming languages, is that common fields have to be defined both in the interface and in its derivative, making the schema a bit more verbose.

A client could query this schema, always deserializing the common fields and conditionally deserializing the rest, as follows.

```graphql
query {
  publications {
    id
    title
    publishedYear
    ... on Book {
      author {
        name
      }
    }
    ... on Magazine {
      issueNumber
    }
    ... on Newspaper {
      date
    }
  }
}

```

Unions provide a similar solution, allowing a type to represent one of several other types.

Assuming that `Book`, `Magazine` and `Newspaper` didn't have a common subset of fields, an interface could technically still be used, but a union would be a better tool for this schema definition.

```graphql
union Publication = Book | Magazine | Newspaper

type Query {
  publications: [Publication!]!
}
```

In this case, the client deserializes all fields conditionally.

```graphql
query {
  publications {
    ... on Book {
      id
      title
      publishedYear
      author {
        name
      }
    }
    ... on Magazine {
      id
      title
      publishedYear
      issueNumber
    }
    ... on Newspaper {
      id
      title
      publishedYear
      date
    }
  }
}
```

## Directives

Directives are annotations, which can be used inside the schema, in order to provide additional functionality to the schema definition.

A common use case is field deprecation.

```graphql
type Author {
  id: ID!
  name: String!
  books: [Book!]!
  bio: String @deprecated(reason: "The field 'about' should be used instead")
  about: String
}
```

Custom directives can be used to provide validation logic. For example, the following, custom `@length` directive enforces a minimum and maximum length on a string field.

```graphql
directive @length(min: Int, max: Int) on FIELD_DEFINITION

type Book implements Publication {
  id: ID!
  title: String! @length(min: 1, max: 100)
  publishedYear: Int!
  author: Author!
}
```

Finally, directives can also be used on the client side, when issuing a query. A typical example is the `@include` directive, which dictates whether a certain field should be included in the response. An example would be the following.

```graphql
query GetBooks($includePublishedYear: Boolean!) {
  books {
    id
    title
    publishedYear @include(if: $includePublishedYear)
    author {
      id
      name
    }
  }
}
```

## Conclusion

A GraphQL schema is a powerful tool, which allows a client to navigate in a graph of data. The objects constitutes the nodes of the graph and the relationships among them define the edges. Read and write operations are explicitly separated, arguments provide filtering and sorting capabilities and directives attach additional functionality to the schema. Finally, elaborate abstractions are powered by  interfaces and unions.
