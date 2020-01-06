# GraphQL Concepts

## Instructions

1. Augment your output from the previous task and apply the concepts stated in this document.

2. Add the following new types:

```graphql
scalar DateTime

enum PROPERTY_TYPE {
  RESIDENTIAL
  COMMERCIAL
  INDUSTRIAL
  LAND
}

type Property {
  uid: ID!
  kind: PROPERTY_TYPE!
  location: String!
  dateAcquired: DateTime!
}
```

_Note: You will need to add a resolver for your scalar `DateTime`._

3. Add the new field `properties` to type `User`:

```graphql
type User {
  id: ID!
  email: String!
  name: String
  properties: [Property!]!
}
```

5. Add the following mutations indicated documented [here](graphql_concepts_api.md).

6. Refer to the concepts in the following section and apply each.

## Concepts

### Directives

Use a directive for user token authentication.

### Type and Field Resolvers

Add a resolver for the type `User`. In your type resolver, also add a resolver for the field `properties`.

### Interfaces

Refactor the type `Property` to use interfaces for each property kind. Also, remove enum `PROPERTY_TYPE`.

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

### Adding Parameters to Field Resolvers

Add an optional parameter named `after` to your field resolver `properties` in your type `User`. This optional property should be used to filter only the properties acquired _after_ a specified date.

```graphql
type User {
  id: ID!
  email: String!
  name: String
  properties(after: DateTime): [Property!]!
}
```
