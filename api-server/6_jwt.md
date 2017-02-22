# Authentication with JWT tokens

JSON Web Tokens are created by encrypted the userID using a secret string. To validate the token we decrypt
the token using the secret string and get the userID.

Install `jwt-simple` using the command:
`npm install --save jwt-simple`

Create a new file `config.js` and add the following snippet:

```javascript
// Holds application secrets and config
module.exports = {
  secret: 'sdkjnfwaeio3roi3jroij' // some random sequence of characters
}
```

The secret must never be exposed to the outside world, so in `.gitignore` file add the entry for `config.js`

Go to `authentication.js` and import `jwt-simple` and `config` :

```javascript
const jwt = require('jwt-simple');
const config = require('../config');
```

Add the jwt creation logic:

```javascript
function tokenForUser(user) {
  const timestamp = new Date().getTime();
  return jwt.encode({ sub: user.id, iat: timestamp }, config.secret);
}
```

Replace the dummy response with the jwt

```javascript
user.save(function(err) {
  if (err) { return next(err); }

  // Respond to request indicating the user was created
  res.json({ token: tokenForUser(user)});
});
```

Try this out in Postman, and verify that a token is returned in response

## Next Up

[Handling login with passport](7_passport.md)


