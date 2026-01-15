# Express.js Examples

## Basic Server Setup
```javascript
const express = require('express');
const helmet = require('helmet');
const rateLimit = require('express-rate-limit');

const app = express();

// Security middleware
app.use(helmet());

// Rate limiting
const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100 // limit each IP to 100 requests per windowMs
});
app.use(limiter);

// Body parsing
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// Routes
app.use('/api/users', userRoutes);

// Error handling middleware
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ error: 'Something went wrong!' });
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

## Async/Await Controller
```javascript
const userService = require('../services/userService');

exports.createUser = async (req, res, next) => {
  try {
    const { name, email } = req.body;
    
    // Input validation
    if (!name || !email) {
      return res.status(400).json({ error: 'Name and email are required' });
    }
    
    const user = await userService.createUser({ name, email });
    res.status(201).json(user);
  } catch (error) {
    next(error);
  }
};
```

## MongoDB Service
```javascript
const User = require('../models/User');

exports.createUser = async (userData) => {
  const user = new User(userData);
  return await user.save();
};

exports.findById = async (id) => {
  return await User.findById(id);
};

exports.findByEmail = async (email) => {
  return await User.findOne({ email });
};
```