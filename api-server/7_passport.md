# Authentication with Passport

[Passport](http://passportjs.org/) is an ecosystem of authentication strategies.
A strategy is a method of authenticating.

Install:

`npm install --save passport passport-jwt`

Create a new folder called `services` and a new file inside it called `passport.js` and populate the following code:

```javascript
const passport = require('passport');
const User = require('../models/user');
const Config = require('../config');
const JwtStrategy = require('passport-jwt').Strategy;
const ExtractJwt = require('passport-jwt').ExtractJwt;

// Setup options for JWT Srategy
const jwtOptions = {
  jwtFromRequest: ExtractJwt.fromHeader('authorization'),
  secretOrKey: config.secret
};

// Create JWT strategy
const jwtLogin = new JwtStrategy(jwtOptions, function(payload, done) {
  // See if the user ID in the payload exists in our databse
  // If it does, call 'done' with that other
  // otherwise, call done without a user
  User.findById(payload.sub, function(err, user) {
    if (err) { return done(err, false); }

    if (user) {
      done(null, user);
    }
    else {
      done(null, false)
    }
  });
});

// Tell passport to use this strategy
passport.use(jwtLogin);
```

In `router.js`, add the following imports

```javascript
const passportService = require('./services/passport');
const passport = require('passport');
```

Create and use the passport authentication middleware
```javascript
const requireAuth = passport.authenticate('jwt', { session: false});

module.exports = function(app) {
  app.get('/', requireAuth, function(req, res) {
    res.send({ hi: 'there' });
  });
  app.post('/signup', Authentication.signup);
}
```

Test theses changes with Postman

## Next up
[Implementing the login functionality]('9_signin.md')

