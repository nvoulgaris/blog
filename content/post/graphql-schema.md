+++
title = "The Anatomy of a GraphQL Schema"
date = "2024-06-17"
image = "img/posts/graphql_introduction.jpeg"
tags = ["GraphQL"]
description = "The Blueprint for Graph Data access"
+++

One of the key features of GraphQL is that it is client-driven.

## Types

### Objects
The objects represent the nodes of the graph. They are the primary building blocks of a GraphQL schema, as they define the structure of the data. An object definition also contains the fields that this object has.

Example:
```graphql
type Book {
  id: ID!
  title: String!
  publishedYear: Int!
}
```

### Scalars
Scalar types are the primitive data types, which are used to define the type of fields. GraphQL supports the following:

 * `String`
 * `Int`
 * `Float`
 * `Boolean`
 * `ID`

These may cover the needs of a basic schema, but it is aparent that they don't suffice for more advanced use cases. For instance, there is no support for dates. However, this is easily solved, as GraphQL allows the definition of custom scalars.

### Enums
Enums are inherently supported.

Example:
```graphql
enum BookType {
  PAPERBACK
  HARDCOVER
}
```

### Lists and Non-Null
While objects, scalars and enums are the only kinds of types that can be defined in a GraphQL schema, there are also a few type modifiers that can be used with them.

Nullability is explicitly declared, by the absence of the Non-Null, `!` modifier. So, `title: String` permits null values, whereas `title: String!` disallows them.

The list modifier `[]` declares an array of the given types. So, for example `books: [Book!]!` refer to a non-null list of non-null books.

## Root types

The root types are the entry points to the schema for the client. These (and only these) can be used to access the graph data and the intention behind them is well defined, separating read from write access points.

### Query

The `Query` type defines read-only operations. 

Example:
```graphql
type Query {
  books: [Book!]!
  book(id: ID!): Book
  authors: [Author!]!
  author(id: ID!): Author
}
```

### Mutation

The `Mutation` type is used to define entry points that result in state modifications.

Example:
```graphql
type Mutation {
  createBook(title: String!, authorId: ID!, publishedYear: Int): Book!
  createAuthor(name: String!): Author!
}
```

### Subscription

The third and last root type is the `Subscription` type, which is used to provide access to real-time updates

Example:
```graphql
type Subscription {
  bookCreated: Book!
}
```

## Relationships

As already explained, the objects represent the nodes of the graph. Additionally, an object may refer to another one and these relationships define the edges of the graph.

Example:
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

## Arguments

## Input types

## Interfaces and Unions

Interfaces, similar to many Object-Oriented prorgamming languages that support them, are abstract types that other types can implement.

Example:
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

```

Unlike usually in programming languages, common fields have to be defined both in the interface and its derivative, making the schema a bit more verbose.

Unions provide a similar solution, allowing a type to represent one of several other types.

Example:
```graphql
union SearchResult = Book | Magazine | Newspaper

type Query {
  searchPublications(keyword: String!): [SearchResult!]!
}
```

## Directives

Directives are annotations, which can be used inside the schema, in order to provide additional functionality to the schema definition.

A common use case is field deprecation.

Example:
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

Finally, directives can also be used in the client side, when issuing a query. A typical example is the `@include` directive, which dictates whether a certain field should be included in the response.

## Conclusion

GraphQL...
