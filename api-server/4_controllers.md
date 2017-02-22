# Creting Controllers

In this section we will be creting controllers in our application that will handle getting and saving user data into mongoDB.

Create a new folder called `controllers` in the project root directory and add a new
file `authentication.js` in it.

Add the following snippet to return a dummy response for now:

```javascript
exports.signup = function(req, res, next) {
  res.send({ success : true });
}
```

In `router.js` replace the existing content with:

```javascript
const Authentication = require('./controllers/authentication');

module.exports = function(app) {
  app.post('/signup', Authentication.signup);
}
```

Go to Postman and do a POST request to the URL `localhost:3090/signup` and verify that you get `{ "success": "true"}` in the response.

We now implement the `signup` route. In `controllers/authentication.js` replace with the following:

```javascript
const User = require('../models/user');

exports.signup = function(req, res, next) {
  const email = req.body.email;
  const password = req.body.password;

  if (!email || !password) {
    return res.status(422).send({ error: "You must provide email and password" });
  }

  // See if a user exists with the given email and address
  User.findOne({ email: email }, function(err, existingUser) {
    if (err) { return next(err); }

     // If a user with email does exists, return an error
    if (existingUser) {
      return res.status(422).send({ error: 'Email is in use' });
    }

    // If a user with email does not exists, create and save user record
    const user = new User({
      email: email,
      password: password
    });

    user.save(function(err) {
      if (err) { return next(err); }
    });

    // Respond to request indicating the user was created
    res.json({ success: true });
  });
}
```

Try this out in Postman.

## Next up

[Encryptin password with bcrypt](5_bcrypt.md)

