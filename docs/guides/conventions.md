---
title: Naming Conventions
description: Enhance your understanding of naming and casing conventions for GraphQL schema to ensure clarity and consistency in your schema design using Tailcall.
---

## General Naming Principles

1. **Consistency is Key:** Ensure that naming conventions are uniform across your entire schema to maintain clarity and consistency.
2. **Descriptive Over Generic:** Opt for descriptive, specific names rather than broad, generic ones to avoid ambiguity.
3. **Avoid Abbreviations:** Avoid the use of acronyms, initialisms, and abbreviations to keep your schema intuitive and understandable.

## Detailed Naming Cases

### Fields, Arguments, and Directives

**Adopt `camelCase`:** Utilize `camelCase` for field names, argument names, and directive names to achieve a clear, consistent structure.

```graphql
type Query {
  postTitle(userId: Int): String
}

directive @includeIf on FIELD
```

### Types

**Prefer `PascalCase`:** Use `PascalCase` for defining types, enabling easy identification and differentiation.

```graphql
type Post { ... }
enum StatusEnum { ... }
interface UserInterface { ... }
union SearchResult = ...
scalar Date
```

**Enum Values in `SCREAMING_SNAKE_CASE`:** Clearly distinguish enum values by using `SCREAMING_SNAKE_CASE`.

```graphql
enum StatusEnum {
  PUBLISHED
  DRAFT
}
```

## Field Naming Best Practices

### Queries

**Avoid `get` or `list` Prefixes:** Refrain from using prefixes like `get` or `list` in your query names to ensure predictability and consistency.

```graphql
type Query {
  # 👎 Avoid
  getPosts: [Post]

  # 👍 Prefer
  posts: [Post]
}
```

Maintain consistency between root and nested fields:

```graphql
# 👎 Avoid
query PostQuery {
  getPosts {
    id
    getUser {
      name
    }
  }
}

# 👍 Prefer
query PostQuery {
  posts {
    id
    user {
      name
    }
  }
}
```

### Mutations

**Verb Prefixes for Mutations:** Begin mutation field names with a verb to clearly indicate the action being performed, improving schema readability.

```graphql
type Mutation {
  # 👎 Avoid
  postAdd(input: AddPostInput): AddPostPayload!

  # 👍 Prefer
  addPost(input: AddPostInput): AddPostPayload!
}
```

## Type Naming Conventions

### Input Types

**`Input` Suffix:** Clearly denote input types by appending `Input` to their names, specifying their use case.

```graphql
input AddPostInput {
  title: String!
  body: String!
  userId: Int!
}
```

### Output Types

**`Response` or `Payload` Suffix:** Use a consistent suffix like `Response` or `Payload` for the output types resulting from mutations.

```graphql
type Mutation {
  addPost(input: AddPostInput!): AddPostResponse!
}

type AddPostResponse {
  success: Boolean!
  post: Post
}
```

## Advanced Naming Strategies

### Resolving Namespace Conflicts

For addressing naming conflicts across different domains within your schema:

**Use `PascalCase` Prefix:** Distinguish similar types from distinct domains for clear separation without resorting to underscores. This method ensures a cleaner, more professional look while maintaining the integrity and readability of your schema.

```graphql
type BlogPost { ... }
type ForumPost { ... }
```

## Conclusion

Implementing a consistent, descriptive, and intuitive naming convention is crucial for developing an understandable and maintainable GraphQL schema. By following the best practices outlined you can improve the clarity and effectiveness of your schema.
