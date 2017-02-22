# Route handling

In this section, we setup the server to handle requests.

## Creating a router

* Create a new file `router.js` 
* Import the new file into `index.js` and invoke it.

```javascript
const router = require('./router');

router(app);
```

In `router.js`

```javascript
module.exports = function(app) {
  app.get('/', function(req, res, next) {
    res.send({ hi: "there" })
  });
}
```

**NOTE:**: `req` and `res` correspond to request and respond. `next` is primarily used for error handling.

Access `localhost:3090` from the broweser and notice that the response JSON shows up.

## Next up
[Set up mongoDB](3_mongo.md)