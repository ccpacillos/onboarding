# GraphQL Concepts

## Instructions

1. Augment your output from the previous task and apply the following concepts.

## Concepts

### Directives

1. Use a `FIELD_DEFINITION` directive for user token authentication.
2. This directive should be used for protected mutations and queries.

### Interfaces

1. Add the following types:

```graphql
interface Property {
  uid: ID!
  location: String!
  dateAcquired: DateTime!
}

type ResidentialProperty implements Property {
  uid: ID!
  location: String!
  dateAcquired: DateTime!
  propertyUniqueToResidential: String!
}

type CommercialProperty implements Property {
  uid: ID!
  location: String!
  dateAcquired: DateTime!
  propertyUniqueToCommercial: Int!
}

type IndustrialProperty implements Property {
  uid: ID!
  location: String!
  dateAcquired: DateTime!
  propertyUniqueToIndustrial: String!
}

type LandProperty implements Property {
  uid: ID!
  location: String!
  dateAcquired: DateTime!
  propertyUniqueToLand: Int!
}
```

_Note: You will need to add a resolver for your scalar `DateTime`._

2. In your `User` type, add the new field `properties`:

```graphql
type User {
  id: ID!
  email: String!
  name: String
  properties: [Property!]!
}
```

3. Add the following mutations documented [here](graphql_concepts_api.md).

### Type and Field Resolvers

1. Add a resolver for the field `properties` of type `User`.

### Adding Parameters to Field Resolvers

1. Add an optional parameter named `after` to your field resolver `properties` in your type `User`. This optional property should be used to filter only the properties acquired _after_ a specified date.

```graphql
type User {
  id: ID!
  email: String!
  name: String
  properties(after: DateTime): [Property!]!
}
```
