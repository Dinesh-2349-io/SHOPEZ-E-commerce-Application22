# SHOPEZ-E-commerce-Application22

---

🛒 SHOPEZ – E-commerce Web Application (Full Mini Project)


---

📌 1. Project Overview

SHOPEZ is a full-stack e-commerce web application designed using modern web technologies. It allows users to browse products, manage shopping carts, and place orders securely.

This project demonstrates:

Full-stack development

REST API design

Authentication & authorization

Database integration

Software engineering best practices



---

🎯 2. Objectives

Build a scalable e-commerce platform

Implement secure login system

Manage products and orders

Provide admin control panel

Deploy a working web application



---

🛠️ 3. Tech Stack

Frontend

React.js

HTML5, CSS3

Axios


Backend

Node.js

Express.js


Database

MongoDB (Mongoose)


Tools

Git & GitHub

Postman

VS Code



---

📂 4. Complete Project Structure

shopez/
│
├── client/
│   ├── public/
│   └── src/
│       ├── components/
│       │   ├── Navbar.js
│       │   ├── ProductCard.js
│       │   └── Cart.js
│       │
│       ├── pages/
│       │   ├── Home.js
│       │   ├── Login.js
│       │   ├── Register.js
│       │   └── ProductDetails.js
│       │
│       ├── App.js
│       └── index.js
│
├── server/
│   ├── models/
│   │   ├── User.js
│   │   ├── Product.js
│   │   └── Order.js
│   │
│   ├── controllers/
│   │   ├── userController.js
│   │   ├── productController.js
│   │   └── orderController.js
│   │
│   ├── routes/
│   │   ├── userRoutes.js
│   │   ├── productRoutes.js
│   │   └── orderRoutes.js
│   │
│   ├── middleware/
│   │   └── authMiddleware.js
│   │
│   └── server.js
│
├── docs/
│   ├── screenshots/
│   └── api-docs.md
│
├── .env.example
├── .gitignore
├── README.md
└── package.json


---

🔐 5. Backend Implementation (Detailed)

📌 server.js

const express = require('express');
const mongoose = require('mongoose');
const dotenv = require('dotenv');
const cors = require('cors');

dotenv.config();

const app = express();
app.use(express.json());
app.use(cors());

mongoose.connect(process.env.MONGO_URI)
.then(() => console.log("Database Connected"))
.catch(err => console.log(err));

app.use('/api/users', require('./routes/userRoutes'));
app.use('/api/products', require('./routes/productRoutes'));
app.use('/api/orders', require('./routes/orderRoutes'));

app.listen(process.env.PORT, () =>
  console.log(`Server running on port ${process.env.PORT}`)
);


---

👤 User Model

const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
  name: String,
  email: { type: String, unique: true },
  password: String,
  isAdmin: { type: Boolean, default: false }
});

module.exports = mongoose.model('User', userSchema);


---

📦 Product Model

const mongoose = require('mongoose');

const productSchema = new mongoose.Schema({
  name: String,
  price: Number,
  description: String,
  image: String,
  countInStock: Number
});

module.exports = mongoose.model('Product', productSchema);


---

🧾 Order Model

const mongoose = require('mongoose');

const orderSchema = new mongoose.Schema({
  user: { type: mongoose.Schema.Types.ObjectId, ref: 'User' },
  products: Array,
  totalPrice: Number,
  isDelivered: Boolean
});

module.exports = mongoose.model('Order', orderSchema);


---

🔑 Authentication Middleware

const jwt = require('jsonwebtoken');

module.exports = function(req, res, next) {
  const token = req.header('Authorization');

  if (!token) return res.status(401).send("Access Denied");

  try {
    const verified = jwt.verify(token, process.env.JWT_SECRET);
    req.user = verified;
    next();
  } catch {
    res.status(400).send("Invalid Token");
  }
};


---

🌐 6. Frontend Implementation

📌 App.js

import React from 'react';
import { BrowserRouter as Router, Route, Routes } from 'react-router-dom';
import Home from './pages/Home';
import Login from './pages/Login';

function App() {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/login" element={<Login />} />
      </Routes>
    </Router>
  );
}

export default App;


---

🛍️ Product Card Component

function ProductCard({ product }) {
  return (
    <div>
      <img src={product.image} alt="" width="150" />
      <h3>{product.name}</h3>
      <p>₹{product.price}</p>
      <button>Add to Cart</button>
    </div>
  );
}

export default ProductCard;


---

🔄 7. API Endpoints

Users

POST /api/users/register

POST /api/users/login


Products

GET /api/products

POST /api/products (Admin)


Orders

POST /api/orders

GET /api/orders



---

🗄️ 8. Database Design

Users Table

id

name

email

password

isAdmin


Products Table

id

name

price

stock


Orders Table

id

user

products

totalPrice



---

⚙️ 9. Installation Guide

# Clone repository
git clone https://github.com/yourusername/shopez.git

# Backend
cd server
npm install

# Frontend
cd ../client
npm install

# Run
cd server && npm start
cd client && npm start


---

📸 10. Screenshots to Add

Home Page

Product Listing

Cart Page

Login/Register

Admin Dashboard



---

📊 11. Software Engineering Concepts Used

MVC Architecture

RESTful APIs

Authentication (JWT)

Database normalization

Version control (Git)



---

🔮 12. Future Enhancements

Payment Gateway (Razorpay/Stripe)

Wishlist feature

Reviews & Ratings

AI-based recommendations



---

📄 13. GitHub README (Final)

🛒 SHOPEZ – E-commerce Web Application

📌 Description

A full-stack e-commerce web application built using MERN stack.

🚀 Features

- Authentication
- Product management
- Cart & Orders

🛠️ Tech Stack

React, Node.js, Express, MongoDB

▶️ Run Locally

npm install
npm start

👨‍💻 Author

Dinesh M
---

🎯 14. Viva / Interview Questions

Prepare these:

What is REST API?

Why MongoDB?

What is JWT?

Explain MVC architecture

How authentication works



---

✅ Final Result

This is now: ✔ College mini project
✔ GitHub-ready project
✔ Resume-level project


---
