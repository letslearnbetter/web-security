# Creating a signin route

Install passport local strategy

`npm install --save passport-local`

In `user.js` add the following snippet

```javascript
userSchema.methods.comparePassword = function(candidatePassword, callback) {
  bcrypt.compare(candidatePassword, this.password, function(err, isMatch {
    if (err) { return callback(err);}

    callback(null, isMatch);
  }))
}
```

In `passport.js` add the following snippet

```javascript
const LocalStrategy = require('passport-local');

// Create local strategy
const localOptions = { usernameField: 'email' ;}
const localLogin = new LocalStrategy(localOptions, function(email, password, done) {
  // Verify this username and password, call done with the user
  // if it is the correct username and password
  // otherwise, call done with false
  User.findOne({ email: email }, function(err, user) {
    if (err) { return done(err); }
    if (!user) { return donr(null, false); }

    // compare passwords - is `password` equal to user.password?
    user.comparePassword(password, function(err, isMatch) {
      if (err) { return done(err); }
      if (!isMatch) { return done(null, false); }

      return done(null, user);
    })
  });
});

passport.use(localLogin);
```

In `router.js`,

```javascript
const requireSignin = passport.authenticate('local', { session: false });
```

Also, add the signing route:
```javascript
app.post('/signin', requireSignin, Authentication.signin);
```

In `authetication.js`
```javascript
exports.signin = function(req, res, next) {
  // User has already had their email and password auth'd
  // We just need to give them a token.
  res.send({ token: tokenForUser(req.user)});
}
```