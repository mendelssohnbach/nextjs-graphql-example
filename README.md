# Building a GraphQL server in Next.js

[Youtube](https://www.youtube.com/watch?v=Hn5neKIfJs8)

```shell
$ npm ls
├── apollo-server-micro@2.25.0
├── dataloader@2.0.0
├── knex@0.20.15
├── micro-cors@0.1.1
├── next@9.5.5
├── pg@7.18.2
├── react-dom@16.14.0
└── react@16.14.0
```

`http://localhost:3001/api/graphql`

```js
import { ApolloServer, gql } from 'apollo-server-micro';

const typeDefs = gql`
  type Query {
    hello: String!
  }
`;

const resolvers = {
  Query: {
    hello: (_parent, _args, _context) => {
      return 'Hello!';
    },
  },
};

const apolloServer = new ApolloServer({
  typeDefs,
  resolvers,
});

const handler = apolloServer.createHandler({ path: '/api/graphql' });

export const config = {
  api: {
    bodyParser: false,
  },
};

export default handler;
```

```
query {
  hello
}

{
  "data": {
    "hello": "Hello!"
  }
}
```

