## setup
```
  npm init -y

  npm i @hapi/hapi

  create /src/server.js
  
```

## boilerplate
```
import Hapi from '@hapi/hapi';

const start = async () => {
    const server = Hapi.server({
        port: 8000,
        host: 'localhost',
    });

    server.route({
      method: 'GET',
      path: '/hello',
      handler: (req, h) => {
          return h.response('Hello').code(201);
      },
    });

    server.route({
      method: 'POST',
      path: '/hello',
      handler: (req, h) => {
          const payload = req.payload;
          const name = payload.name;
          return `Hello ${name}!`;
      },
    });

    await server.start();
    console.log(`Server is listening on ${server.info.uri}`);
}

process.on('unhandledRejection', err => {
    console.log(err);
    process.exit(1);
});

start();
```

## Error handling
```
  npm i @hapi/boom
```

Send error to client
```
  if (user.user_id !== userId) 
    throw Boom.unauthorized('Users can only access their own listings!');


  if (!listing) 
    throw Boom.notFound(`Listing does not exist with id ${id}`);    // 404
```



## Run
```
  npx babel-node src/server.js
```

## Auto restart
```
  npm i --save-dev nodemon
```
npm secript
```
  "dev": "nodemon --exec babel-node src/server.js",
```


