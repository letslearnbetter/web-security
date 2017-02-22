# Password encryption

Storing passwords as plain text is a huge security vulnerability. If a maliciout actor ever got In this section we will use the bcrypt library
to encrypt our passwords before saving them in the database.

Install bcrypt
`npm install --save bcrypt-nodejs`

In `models/user.js` add the following snippet.

```javascript
const bcrypt = require('bcrypt-nodejs);

// On Save Hookl, encrypt password
// Before saving a model, run this function
userSchema.pre('save', function(next) {
  // get access to the user model
  const user = this;

  // generate a salt, then run callback
  bcrypt.genSalt(10, function(err, salt) {
    if (err) { return next(err); }

    // hash (encrypt) our password using the salt
    bcrypt.hash(user.password, salt, null, function(err, hash) {
      if (err) { return next(err); }

      // overwrite plain text password with the encrypted password
      user.password = hash;
      next();
    });
  });
});
```

Create a new password in Postman and verify that the password is encrypted in Robomongo

## Next Up
[JWT](6_jwt.md)

