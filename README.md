🛒 SHOPEZ : E-commerce Application

---

📌 PROJECT ARCHITECTURE

🔷 Overall Architecture

Client (React.js)
        ↓
API Layer (Node.js + Express)
        ↓
Database (MongoDB)

Frontend → React (UI)

Backend → Node.js + Express (API)

Database → MongoDB (NoSQL)



---

⚙️ TECHNICAL ARCHITECTURE

Layer	Technology Used

Frontend	React.js, Axios, Bootstrap
Backend	Node.js, Express.js
Database	MongoDB, Mongoose
Auth	JWT (JSON Web Token)
Tools	Git, Postman



---

🧩 ER DIAGRAM (Text Representation)

User
 ├── userId
 ├── name
 ├── email
 └── password

Product
 ├── productId
 ├── name
 ├── price
 └── category

Order
 ├── orderId
 ├── userId
 ├── products[]
 └── totalAmount

Relationships:

User → places → Order

Order → contains → Product



---

✨ FEATURES

🔐 User Authentication (Login/Register)

🛍️ Product Listing

🛒 Add to Cart

💳 Order Placement

📦 Order History

🔍 Search & Filter

🧑 Admin Dashboard (Add/Edit/Delete Products)



---

👥 ROLES AND RESPONSIBILITIES

👤 User

Register/Login

Browse Products

Add to Cart

Place Orders


🛠️ Admin

Manage Products

View Orders

Manage Users



---

🔄 USER FLOW

Register → Login → Browse Products → Add to Cart → Checkout → Order Confirmation


---

🧱 MVC PATTERN

Layer	Description

Model	MongoDB Schemas
View	React UI
Controller	Business Logic (Express APIs)



---

🛠️ PROJECT SETUP AND CONFIGURATION

📁 Creating Project Folder

shopez/
├── client/
├── server/


---

💻 Client Setup (React)

npx create-react-app client
cd client
npm install axios react-router-dom
npm start


---

🖥️ Server Setup (Node)

mkdir server
cd server
npm init -y
npm install express mongoose cors dotenv jsonwebtoken bcryptjs


---

🚀 BACKEND DEVELOPMENT

📁 BACKEND STRUCTURE

server/
├── config/
│   └── db.js
├── models/
│   ├── User.js
│   ├── Product.js
│   └── Order.js
├── routes/
│   ├── userRoutes.js
│   ├── productRoutes.js
│   └── orderRoutes.js
├── controllers/
│   ├── userController.js
│   ├── productController.js
│   └── orderController.js
├── middleware/
│   └── authMiddleware.js
├── server.js
└── .env


---

🔧 DEVELOPMENT AND EXPLANATION

server.js

const express = require('express');
const mongoose = require('mongoose');
const cors = require('cors');
require('dotenv').config();

const app = express();

app.use(express.json());
app.use(cors());

mongoose.connect(process.env.MONGO_URI)
.then(() => console.log("MongoDB Connected"))
.catch(err => console.log(err));

app.use('/api/users', require('./routes/userRoutes'));
app.use('/api/products', require('./routes/productRoutes'));
app.use('/api/orders', require('./routes/orderRoutes'));

app.listen(5000, () => console.log("Server running on port 5000"));


---

🗄️ DATABASE DEVELOPMENT

🔗 Configure MongoDB

Create account in MongoDB Atlas

Get connection string



---

🔌 CREATE DATABASE CONNECTION

config/db.js

const mongoose = require('mongoose');

const connectDB = async () => {
    try {
        await mongoose.connect(process.env.MONGO_URI);
        console.log("DB Connected");
    } catch (error) {
        console.error(error);
        process.exit(1);
    }
};

module.exports = connectDB;


---

📦 Create Schema and Models

User Model

const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
    name: String,
    email: String,
    password: String
});

module.exports = mongoose.model('User', userSchema);


---

Product Model

const mongoose = require('mongoose');

const productSchema = new mongoose.Schema({
    name: String,
    price: Number,
    category: String
});

module.exports = mongoose.model('Product', productSchema);


---

Order Model

const mongoose = require('mongoose');

const orderSchema = new mongoose.Schema({
    userId: String,
    products: Array,
    totalAmount: Number
});

module.exports = mongoose.model('Order', orderSchema);


---

🎨 FRONTEND DEVELOPMENT

📁 Frontend Structure

client/
├── src/
│   ├── components/
│   ├── pages/
│   ├── services/
│   ├── App.js
│   └── index.js


---

⚡ Development and Execution

Example API call:

import axios from 'axios';

const fetchProducts = async () => {
    const res = await axios.get('http://localhost:5000/api/products');
    console.log(res.data);
};


---

▶️ PROJECT EXECUTION

🧾 Steps For Execution

1️⃣ Start Backend

cd server
npm install
npm run start

2️⃣ Start Frontend

cd client
npm install
npm start

3️⃣ Open Browser

http://localhost:3000


---

📌 FINAL GITHUB STRUCTURE

shopez/
├── client/        # React Frontend
├── server/        # Node Backend
├── README.md
└── package.json


---

If you want next level 🚀:

I can add JWT authentication full code

Admin dashboard UI

Payment gateway (Stripe/Razorpay)

Deploy to Render / Vercel
