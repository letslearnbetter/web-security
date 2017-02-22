# Setting up MongoDB

We have already installed mongoose, which is used to interface with MongoDB in a previous section.

Create a new folder `models` and a new file `user.js` inside it.

```javascript
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

// Define the model
const userSchema = new Schema({
  email: { type: String, unique: true, lowercase: true },
  password: String
});

// Create the model class
const ModelClass = mongoose.model('user', userSchema); // Loads the schema into mogoose and maps it to a collection called user

// Export the model
module.exports = ModelClass;
```

Ensure that the mongoDB is running by running the command `mongod`

Wire up mongoose to listen to mongoDB. Inside `index.js` add the folliwing snippet

```javascript
const mongoose = require('mongoose');

// DB Setup
mongoose.connect('mongodb://localhost:auth/auth'); // Creates a new database in mongoDB called auth
```

## Next Up

[Creating controllers to handle incoming requests](4_controllers.md)