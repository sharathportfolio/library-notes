# Mongoose and MongoDB Packages

## 1. `mongoose`

Mongoose is an Object Data Modeling (ODM) library for MongoDB and Node.js. It provides schemas, models, validation, middleware, and query methods to interact with MongoDB.

### Installation

```bash
npm install mongoose
```

### Import

```javascript
const mongoose = require("mongoose");
```

Or using ES modules:

```javascript
import mongoose from "mongoose";
```

### Connect to MongoDB

```javascript
const mongoose = require("mongoose");

const connectDB = async () => {
  try {
    await mongoose.connect("mongodb://127.0.0.1:27017/mydatabase");
    console.log("MongoDB connected");
  } catch (error) {
    console.error("MongoDB connection error:", error);
    process.exit(1);
  }
};

module.exports = connectDB;
```

### Create a Schema

A schema defines the structure and validation rules of documents.

```javascript
const userSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true
  },
  email: {
    type: String,
    required: true,
    unique: true
  },
  age: {
    type: Number,
    min: 18
  }
}, {
  timestamps: true
});
```

### Create a Model

A model is used to interact with a MongoDB collection.

```javascript
const User = mongoose.model("User", userSchema);

module.exports = User;
```

### CRUD Operations

**Create**

```javascript
const user = await User.create({
  name: "John",
  email: "john@example.com",
  age: 25
});
```

**Find all documents**

```javascript
const users = await User.find();
```

**Find one document**

```javascript
const user = await User.findOne({
  email: "john@example.com"
});
```

**Find by ID**

```javascript
const user = await User.findById(userId);
```

**Update a document**

```javascript
const user = await User.findByIdAndUpdate(
  userId,
  { name: "John Updated" },
  { new: true, runValidators: true }
);
```

**Delete a document**

```javascript
const user = await User.findByIdAndDelete(userId);
```

### Common Mongoose Methods

| Method | Purpose |
|---|---|
| `mongoose.connect()` | Connect to MongoDB |
| `mongoose.Schema()` | Define document structure |
| `mongoose.model()` | Create a model |
| `Model.create()` | Insert a document |
| `Model.find()` | Find multiple documents |
| `Model.findOne()` | Find one document |
| `Model.findById()` | Find by ID |
| `Model.findByIdAndUpdate()` | Update by ID |
| `Model.findByIdAndDelete()` | Delete by ID |
| `document.save()` | Save document changes |
| `document.populate()` | Load referenced documents |
| `Model.aggregate()` | Run aggregation pipelines |

---

## 2. `mongodb-memory-server`

`mongodb-memory-server` starts a temporary MongoDB server that runs locally for testing. It allows developers to test MongoDB operations without connecting to a separate database server.

### Installation

```bash
npm install --save-dev mongodb-memory-server
```

### Import

```javascript
const { MongoMemoryServer } = require("mongodb-memory-server");
```

### Start an In-Memory MongoDB Server

```javascript
const mongoose = require("mongoose");
const { MongoMemoryServer } = require("mongodb-memory-server");

let mongoServer;

const connectDB = async () => {
  mongoServer = await MongoMemoryServer.create();

  const mongoUri = mongoServer.getUri();

  await mongoose.connect(mongoUri);

  console.log("In-memory MongoDB connected");
};

const disconnectDB = async () => {
  await mongoose.disconnect();

  if (mongoServer) {
    await mongoServer.stop();
  }
};

module.exports = {
  connectDB,
  disconnectDB
};
```

### Use with Jest

Example test:

```javascript
const mongoose = require("mongoose");
const { MongoMemoryServer } = require("mongodb-memory-server");

let mongoServer;

beforeAll(async () => {
  mongoServer = await MongoMemoryServer.create();

  await mongoose.connect(mongoServer.getUri());
});

afterEach(async () => {
  const collections = mongoose.connection.collections;

  for (const key of Object.keys(collections)) {
    await collections[key].deleteMany({});
  }
});

afterAll(async () => {
  await mongoose.disconnect();
  await mongoServer.stop();
});
```

### Example Model Test

```javascript
const User = require("../models/user");

describe("User Model", () => {
  it("creates a user successfully", async () => {
    const user = await User.create({
      name: "John",
      email: "john@example.com",
      age: 25
    });

    expect(user.name).toBe("John");
    expect(user.email).toBe("john@example.com");
  });
});
```

### Common Uses

- Testing Mongoose models.
- Testing Express API endpoints.
- Running integration tests.
- Testing database queries.
- Avoiding a separate MongoDB test database.

**Note:** The package may download a MongoDB binary when first used. Internet access may be required unless the binary is already available locally.

---

## 3. `mongoose-update-if-current`

`mongoose-update-if-current` is a Mongoose plugin that helps prevent conflicting document updates using optimistic concurrency control.

It uses the document version key (`__v`) to detect whether another update has modified a document before saving.

### Installation

```bash
npm install mongoose-update-if-current
```

### Import

```javascript
const mongoose = require("mongoose");
const updateIfCurrentPlugin = require("mongoose-update-if-current");
```

### Apply the Plugin

```javascript
const userSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true
  },
  email: {
    type: String,
    required: true
  }
});

userSchema.plugin(updateIfCurrentPlugin);

const User = mongoose.model("User", userSchema);

module.exports = User;
```

### Example: Optimistic Concurrency

Suppose two users retrieve the same document.

```javascript
const userOne = await User.findById(userId);
const userTwo = await User.findById(userId);
```

Both documents initially have the same version.

The first user updates and saves:

```javascript
userOne.name = "Updated by User One";

await userOne.save();
```

The second user tries to save an outdated document:

```javascript
userTwo.name = "Updated by User Two";

await userTwo.save();
```

The second save can fail with a version conflict because the document has already been updated.

### Why Use It?

- Prevents lost updates.
- Detects stale document versions.
- Helps protect data from concurrent modifications.
- Useful in applications where multiple users edit the same document.

**Important:** This plugin is designed for document `save()` operations. Do not assume it automatically protects every update method, such as `findByIdAndUpdate()` or `updateOne()`. Check the plugin's compatibility with your Mongoose version and its current documentation.

---

## 4. Quick Comparison

| Package | Purpose |
|---|---|
| `mongoose` | ODM for MongoDB |
| `mongodb-memory-server` | Temporary MongoDB server for testing |
| `mongoose-update-if-current` | Optimistic concurrency control |

## 5. Typical Project Structure

```text
my-project/
│
├── models/
│   └── user.js
│
├── database/
│   └── connect.js
│
├── tests/
│   └── user.test.js
│
├── app.js
├── package.json
└── README.md
```

## 6. Important Notes

- Use Mongoose schemas to define document structure and validation.
- Use `mongodb-memory-server` for isolated database integration tests.
- Use optimistic concurrency when multiple users may update the same document.
- Keep MongoDB connection strings and credentials in environment variables.
- Remember that an in-memory MongoDB instance is temporary and should not be used as production storage.
- Mongoose also provides built-in optimistic concurrency through the schema option `optimisticConcurrency: true`, which may be preferable to adding a separate plugin.

## Official Documentation

- Mongoose: https://mongoosejs.com/
- MongoDB Memory Server: https://github.com/typegoose/mongodb-memory-server
- Mongoose Update If Current: https://www.npmjs.com/package/mongoose-update-if-current
- MongoDB: https://www.mongodb.com/docs/