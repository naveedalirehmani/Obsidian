  

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
