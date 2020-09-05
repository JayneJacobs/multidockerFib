# Worker
in worker Directory
1. set up package.json dependancies
   - nodemon
   - redis
  Add scripts
2. Create index.js
   - const keys = require('./keys)
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
