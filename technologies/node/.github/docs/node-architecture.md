# Node.js Architecture Patterns

## MVC Pattern

```
src/
├── controllers/
│   ├── userController.js
│   └── productController.js
├── models/
│   ├── User.js
│   └── Product.js
├── routes/
│   ├── userRoutes.js
│   └── productRoutes.js
├── services/
│   ├── userService.js
│   └── productService.js
├── middleware/
│   ├── auth.js
│   └── validation.js
└── utils/
    ├── logger.js
    └── database.js
```

## Microservices Pattern

```javascript
// Main gateway service
const express = require('express');
const axios = require('axios');

const app = express();

app.get('/api/composite/:userId', async (req, res) => {
  try {
    const { userId } = req.params;
    
    // Parallel calls to microservices
    const [user, orders, recommendations] = await Promise.all([
      axios.get(`http://user-service/users/${userId}`),
      axios.get(`http://order-service/orders/user/${userId}`),
      axios.get(`http://recommendation-service/recommendations/${userId}`)
    ]);
    
    res.json({
      user: user.data,
      orders: orders.data,
      recommendations: recommendations.data
    });
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});
```

## Event-Driven Architecture

```javascript
// Event emitter for decoupled communication
const EventEmitter = require('events');

class EventBus extends EventEmitter {
  publish(event, data) {
    this.emit(event, data);
  }
  
  subscribe(event, handler) {
    this.on(event, handler);
  }
}

const eventBus = new EventBus();

// Event handlers
eventBus.subscribe('user.created', (user) => {
  console.log(`User created: ${user.email}`);
  // Send welcome email
  // Create default profile
  // Log analytics event
});

// Publishing events
exports.createUser = async (userData) => {
  const user = await User.create(userData);
  eventBus.publish('user.created', user);
  return user;
};
```