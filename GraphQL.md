I   

#### Basic Query: ☑️

- Writing simple queries to fetch data from a GraphQL server.
#### Query Variables: ☑️

- Using variables in queries to make them more dynamic and reusable.
#### Query Aliases: ☑️

- Using aliases to rename fields in the query result.
- This is for the client side where you want to make multiple queries in one query for a one specific resolver. 

```
query {
  user1: user(id: 1) {
    firstName
    lastName
  }

  user2: user(id: 2) {
    firstName
    lastName
  }
}
```

#### Fragments: ☑️

- Creating fragments to reuse common selections in multiple queries.
- This is for client side. We can use this to create a set of fields that are return from 2 or more different queries, instead of rewritting the fields we use fragments. 

```
fragment CommonFields on Person {
  firstName
  lastName
  email
}

query GetUser {
  user(id: 1) {
    ...CommonFields
    age
  }
}

query GetEmployee {
  employee(id: 1) {
    ...CommonFields
    jobTitle
  }
}
```

#### Nested Queries: ☑️

- Fetching nested data by specifying subfields in the query.
#### Arguments: ☑️

- Passing arguments to queries to filter, paginate, or customize the data.
- Passing in variables :)
#### Basic Mutation: ☑️

- Writing mutations to modify data on the server.
#### Input Types: ☑️

- Using input types in mutations to pass complex data as arguments.
#### Enums: ☑️

- Defining and using enumeration types to represent a set of possible values.
#### Interfaces and Unions:

- Defining and using interfaces and unions to support polymorphic types.
- Don’t understand.
#### Custom Scalars:

- Creating custom scalar types to handle specific data formats (e.g., Date).
#### Directives:

- Using directives (@include and @skip) to conditionally include or skip fields.
#### Resolvers: ☑️

- Understanding and implementing resolvers to fetch data from various sources.
#### Schema Design: ☑️

- Designing GraphQL schemas with appropriate types, queries, and mutations.
#### Schema Stitching/Federation: ☑️

- Integrating multiple GraphQL services into a single schema using stitching or federation.
#### Pagination and Cursors: ☑️

- Implementing pagination with GraphQL using cursor-based or offset-based approaches.
#### Error Handling: ☑️

- Handling errors in GraphQL queries and mutations and returning informative error messages.
#### Authentication and Authorization:

- Implementing authentication and authorization mechanisms in GraphQL.
#### Caching and Performance Optimization: 

- Optimizing GraphQL queries with caching and batching techniques.
#### Subscriptions:

- Using GraphQL subscriptions to enable real-time data updates.
#### Testing GraphQL APIs:

- Writing unit and integration tests for GraphQL APIs.
#### Best Practices and Security:

- Learning best practices for designing and securing GraphQL APIs.
#### Apollo Client or Relay: ☑️

- Using popular GraphQL client libraries like Apollo Client or Relay.