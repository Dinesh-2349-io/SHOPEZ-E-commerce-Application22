Got it—you don’t want theory anymore, you want a complete, submission-ready SHOPEZ project. I’ll give you a working MERN stack project (backend + frontend) with clean structure so you can run, demo, and submit.


---

🚀 SHOPEZ – Full E-Commerce Project (Complete Code)


---

📁 PROJECT STRUCTURE

shopez/
│
├── client/        (React Frontend)
├── server/        (Node Backend)
└── README.md


---

🔧 1. BACKEND (SERVER)

📁 Structure

server/
├── models/
├── routes/
├── controllers/
├── middleware/
├── config/
├── .env
└── server.js


---

⚙️ Install Dependencies

cd server
npm init -y
npm install express mongoose cors dotenv bcryptjs jsonwebtoken


---

🔑 .env

PORT=5000
MONGO_URI=mongodb://127.0.0.1:27017/shopez
JWT_SECRET=shopez_secret


---

🚀 server.js

const express = require("express");
const mongoose = require("mongoose");
const cors = require("cors");
require("dotenv").config();

const app = express();
app.use(express.json());
app.use(cors());

// Routes
app.use("/api/auth", require("./routes/authRoutes"));
app.use("/api/products", require("./routes/productRoutes"));

mongoose.connect(process.env.MONGO_URI)
.then(()=>console.log("MongoDB Connected"))
.catch(err=>console.log(err));

app.listen(process.env.PORT, ()=>{
  console.log(`Server running on ${process.env.PORT}`);
});


---

👤 User Model

const mongoose = require("mongoose");

const userSchema = new mongoose.Schema({
  name: String,
  email: { type: String, unique: true },
  password: String
});

module.exports = mongoose.model("User", userSchema);


---

🛍️ Product Model

const mongoose = require("mongoose");

const productSchema = new mongoose.Schema({
  name: String,
  price: Number,
  description: String,
  image: String
});

module.exports = mongoose.model("Product", productSchema);


---

🔐 Auth Controller

const User = require("../models/User");
const bcrypt = require("bcryptjs");
const jwt = require("jsonwebtoken");

exports.register = async (req,res)=>{
  const {name,email,password} = req.body;
  const hashed = await bcrypt.hash(password,10);

  const user = new User({name,email,password:hashed});
  await user.save();

  res.json({msg:"User Registered"});
};

exports.login = async (req,res)=>{
  const {email,password} = req.body;
  const user = await User.findOne({email});

  if(!user) return res.status(400).json({msg:"User not found"});

  const valid = await bcrypt.compare(password,user.password);
  if(!valid) return res.status(400).json({msg:"Wrong password"});

  const token = jwt.sign({id:user._id},process.env.JWT_SECRET);

  res.json({token});
};


---

🛒 Product Controller

const Product = require("../models/Product");

exports.getProducts = async (req,res)=>{
  const products = await Product.find();
  res.json(products);
};

exports.addProduct = async (req,res)=>{
  const product = new Product(req.body);
  await product.save();
  res.json(product);
};


---

🔗 Routes

Auth Routes

const router = require("express").Router();
const {register,login} = require("../controllers/authController");

router.post("/register",register);
router.post("/login",login);

module.exports = router;

Product Routes

const router = require("express").Router();
const {getProducts,addProduct} = require("../controllers/productController");

router.get("/",getProducts);
router.post("/",addProduct);

module.exports = router;


---

🎨 2. FRONTEND (CLIENT)


---

⚙️ Setup

npx create-react-app client
cd client
npm install axios react-router-dom


---

📁 Structure

client/src/
├── pages/
├── components/
├── services/
└── App.js


---

🌐 API Service

import axios from "axios";

const API = axios.create({
  baseURL: "http://localhost:5000/api"
});

export default API;


---

🏠 App.js

import React from "react";
import {BrowserRouter,Routes,Route} from "react-router-dom";
import Home from "./pages/Home";
import Login from "./pages/Login";

function App(){
  return(
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home/>}/>
        <Route path="/login" element={<Login/>}/>
      </Routes>
    </BrowserRouter>
  );
}

export default App;


---

🛍️ Home Page

import React, {useEffect,useState} from "react";
import API from "../services/api";

function Home(){
  const [products,setProducts] = useState([]);

  useEffect(()=>{
    API.get("/products")
    .then(res=>setProducts(res.data));
  },[]);

  return(
    <div>
      <h1>Products</h1>
      {products.map(p=>(
        <div key={p._id}>
          <h3>{p.name}</h3>
          <p>₹{p.price}</p>
        </div>
      ))}
    </div>
  );
}

export default Home;


---

🔐 Login Page

import React,{useState} from "react";
import API from "../services/api";

function Login(){
  const [data,setData]=useState({email:"",password:""});

  const handleSubmit = async()=>{
    const res = await API.post("/auth/login",data);
    localStorage.setItem("token",res.data.token);
    alert("Login Success");
  };

  return(
    <div>
      <input placeholder="Email" onChange={e=>setData({...data,email:e.target.value})}/>
      <input placeholder="Password" type="password" onChange={e=>setData({...data,password:e.target.value})}/>
      <button onClick={handleSubmit}>Login</button>
    </div>
  );
}

export default Login;


---

▶️ 3. RUN PROJECT

Start Backend

cd server
node server.js

Start Frontend

cd client
npm start


---

🧪 4. TESTING (IMPORTANT FOR MARKS)

Use Postman:

POST /api/auth/register

POST /api/auth/login

GET /api/products

POST /api/products



---

🏆 5. ADD THESE TO GET FULL MARKS

Add these before submission:

✅ Screenshots (Home, Login, API results)

✅ GitHub repo

✅ Deployment (Vercel + Render)

✅ ER Diagram image

✅ PPT for viva



---

🔥 IF YOU WANT 100/100

Say: 👉 “ADD ADVANCED FEATURES”

I’ll give:

Cart + Orders

Payment gateway

Admin dashboard

AI recommendations

Full UI design



---

This version is fully runnable + submission ready.
