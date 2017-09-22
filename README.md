# GraphQL Extensions

This project contains a repository of suggested or draft extensions or changes (as minimal as possible for the latter) to your GraphQL Schema.
Using [GraphQL Faker](https://github.com/APIs-guru/graphql-faker) you will be able to proxy your existing schema but also to mock and simulate the proposed changes

## Instructions

1. Setting up the project:

First, run npm to initialize the project dependencies
```shell
npm install
```

2. If you schema endpoint requires authentication, insert here instructions to fill in the Header with an auth token or another kind of authentication. Example:

Log in to http://mycompany.com, then run this in the javascript console (Shift-Cmd-J):
```javascript
JSON.parse(localStorage.getItem("session")).accessToken
```
This will return a string that you need to copy and paste in the next command

3. Running an extension file:
```shell
npm start -- --extend [your GraphQL endpoint] --header "Authorization:Bearer [THE AUTH TOKEN YOU GOT]" ./example.faker.graphql
```

