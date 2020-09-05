# Server
in Server Directory
1. set up package.json dependancies
   - cors // Cross Origin Resource Sharing
   - redis
   - pg
   - express
   - nodemon
   - body parser //format body (json)
  Add scripts
  - dev
  - start
2. Create index.js
   - ```js 
      const keys = require('./keys')```

   - create keys.js
   - ```javascript
      retry_strategy: () => 1000```

```javascript
if (index < 2) return 1;
return fib(index - 1) + fib(index - 2);
```
```javascript
sub.on('message', (channel, message)) {
    redisClient.hset('values', message, fib(parseInt(message)));
}
sub.subscribe('insert');
```
