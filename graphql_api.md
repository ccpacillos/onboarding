# GraphQL API Server

## Instructions

Create a new project and convert the [REST API Server](rest_api_server.md) to GraphQL. Endpoints will be listed in the API Specifications below.

## Guidelines

See guidelines [here](guidelines.md).

## API Specifications

### Authentication

#### Login

Login endpoint should be provided using a REST API endpoint as documented [here](rest_api.md#2-authenticate-user).

#### Authentication Header

Protected endpoints should still use `Authorization: Bearer {token}` authentication header.

### GraphQL Schema

```graphql
type User {
  id: ID!
  email: String!
  name: String
}

input CreateUserInput {
  email: String!
  password: String!
  name: String
}

input UpdateProfileInput {
  name: String
  password: String
}

type Mutation {
  createUser(input: CreateUserInput!): User!
  updateProfile(input: UpdateProfileInput!): User!
}

type Query {
  users(): [User!]!
  user(id: ID!): User!
}
```

### Mutations

- `Mutation.createUser`

  - unprotected endpoint
  - creates a new user
  - should respond with an error for duplicate email
  - should respond with an error for email validation errors
  - returns the created user

- `Mutation.updateUser`

  - protected endpoint
  - updates own profile
  - users cannot update other users' profile/information
  - should respond with an error for email validation errors
  - returns the updated user

### Query

- `Query.users`

  - protected endpoint
  - retrieves list of all users

- `Query.user`

  - protected endpoint
  - retrieves a single user specified by an id
