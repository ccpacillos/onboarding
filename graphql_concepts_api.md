# GraphQL Concepts: Additional Mutations

## Mutations

Add the following mutations:

```graphql
type Mutation {
  addProperty(input: AddPropertyInput!): Property!
  removeProperty(uid: ID!): Boolean!
}
```

_Note: You have to provide your own input `AddPropertyInput`._

## Description

### `Mutation.addProperty`

Adds a property to the current user. Accepts a `uid` value from the user that uniquely identifies the property. If the `uid` already exists, return an error.

### `Mutation.removeProperty`

Removes a property of the current user with the provided `uid` value.
