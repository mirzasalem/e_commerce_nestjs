# 🛒 E-Commerce REST API
 
A fully-featured e-commerce backend built with **NestJS**, **TypeORM**, and **MySQL**. This API supports authentication, role-based access control, product management, cart operations, and order processing with full business logic and data consistency.
 
---
 
## 🌐 Live Demo
 
| | URL |
|---|---|
| 🚀 **Base API** | https://mirzasalem-ecommerce.up.railway.app/api |
| 📖 **Swagger Docs** | https://mirzasalem-ecommerce.up.railway.app/api/docs |
 
> Deployed on **Railway** with a managed **MySQL** database.
 
---
 
## 🚀 Tech Stack
 
- **Framework**: NestJS
- **Database**: MySQL
- **ORM**: TypeORM
- **Authentication**: JWT (JSON Web Tokens)
- **Validation**: class-validator & class-transformer
- **API Docs**: Swagger UI
 
---
 
## ✨ Features
 
- ✅ User Registration & Login with JWT
- ✅ Role-based Access Control (Admin / Customer)
- ✅ Product & Category Management (Admin only)
- ✅ Shopping Cart (Add, Remove, View)
- ✅ Order Placement with stock deduction
- ✅ Backend order total calculation
- ✅ Prevent over-ordering (stock validation)
- ✅ Prevent negative inventory
- ✅ Order cancellation with stock restoration
- ✅ Fraud prevention (cancellation limit per user)
- ✅ Order status management (Pending / Shipped / Delivered / Cancelled)
- ✅ Database transactions for data integrity
- ✅ Input validation & error handling
- ✅ Swagger API documentation
 
---
 
## 📁 Project Structure
 
```
src/
├── auth/                   # JWT auth, guards, decorators
│   ├── dto/
│   │   ├── register.dto.ts
│   │   └── login.dto.ts
│   ├── auth.controller.ts
│   ├── auth.service.ts
│   ├── auth.module.ts
│   ├── jwt.strategy.ts
│   ├── roles.decorator.ts
│   ├── roles.enum.ts
│   └── roles.guard.ts
├── users/                  # User entity & service
│   ├── user.entity.ts
│   ├── users.service.ts
│   ├── users.controller.ts
│   └── users.module.ts
├── products/               # Product CRUD (Admin only)
│   ├── dto/
│   │   ├── create-product.dto.ts
│   │   └── update-product.dto.ts
│   ├── product.entity.ts
│   ├── products.controller.ts
│   ├── products.service.ts
│   └── products.module.ts
├── categories/             # Product categories
│   ├── dto/
│   │   └── create-category.dto.ts
│   ├── category.entity.ts
│   ├── categories.controller.ts
│   ├── categories.service.ts
│   └── categories.module.ts
├── cart/                   # Shopping cart
│   ├── dto/
│   │   └── add-to-cart.dto.ts
│   ├── cart.entity.ts
│   ├── cart.controller.ts
│   ├── cart.service.ts
│   └── cart.module.ts
├── orders/                 # Order management
│   ├── dto/
│   │   ├── create-order.dto.ts
│   │   └── update-order-status.dto.ts
│   ├── order.entity.ts
│   ├── order-item.entity.ts
│   ├── orders.controller.ts
│   ├── orders.service.ts
│   └── orders.module.ts
├── app.module.ts
└── main.ts
```
 
---
 
## ⚙️ Installation & Setup
 
### Prerequisites
- Node.js (v18+)
- MySQL
- npm
 
### 1. Clone the repository
```bash
git clone https://github.com/your-username/ecommerce-backend.git
cd ecommerce-backend
```
 
### 2. Install dependencies
```bash
npm install
```
 
### 3. Configure environment variables
Create a `.env` file in the root directory:
```env
# Database
DB_HOST=localhost
DB_PORT=3306
DB_USERNAME=root
DB_PASSWORD=your_mysql_password
DB_NAME=ecommerce
 
# JWT
JWT_SECRET=your_super_secret_jwt_key_here
JWT_EXPIRES_IN=7d
 
# App
PORT=3000
```
 
### 4. Create MySQL database
```sql
CREATE DATABASE ecommerce;
```
 
### 5. Run the application
```bash
# Development
npm run start:dev
 
# Production
npm run build
npm run start:prod
```
 
The server will start at `http://localhost:3000/api` 🚀
 
---
 
## 📖 API Documentation
 
Swagger UI is available at:
```
http://localhost:3000/api/docs
```
 
---
 
## 🔐 Authentication
 
This API uses **JWT Bearer Token** authentication.
 
1. Register or login to get a token
2. Include the token in the `Authorization` header:
```
Authorization: Bearer <your_token>
```
 
---
 
## 📡 API Endpoints
 
### 🔑 Auth
| Method | Endpoint | Access | Description |
|--------|----------|--------|-------------|
| POST | `/api/auth/register` | Public | Register a new user |
| POST | `/api/auth/login` | Public | Login and get JWT token |
 
### 📦 Products
| Method | Endpoint | Access | Description |
|--------|----------|--------|-------------|
| GET | `/api/products` | Public | Get all products |
| GET | `/api/products/:id` | Public | Get product by ID |
| POST | `/api/products` | Admin | Create a new product |
| PATCH | `/api/products/:id` | Admin | Update a product |
| DELETE | `/api/products/:id` | Admin | Delete a product |
 
### 🗂️ Categories
| Method | Endpoint | Access | Description |
|--------|----------|--------|-------------|
| GET | `/api/categories` | Public | Get all categories |
| GET | `/api/categories/:id` | Public | Get category by ID |
| POST | `/api/categories` | Admin | Create a new category |
| PATCH | `/api/categories/:id` | Admin | Update a category |
| DELETE | `/api/categories/:id` | Admin | Delete a category |
 
### 🛒 Cart
| Method | Endpoint | Access | Description |
|--------|----------|--------|-------------|
| GET | `/api/cart` | Customer | View cart with total |
| POST | `/api/cart` | Customer | Add product to cart |
| DELETE | `/api/cart/:id` | Customer | Remove item from cart |
 
### 📋 Orders
| Method | Endpoint | Access | Description |
|--------|----------|--------|-------------|
| POST | `/api/orders` | Customer | Place an order |
| GET | `/api/orders/my-orders` | Customer | Get my orders |
| GET | `/api/orders/:id` | Both | Get order by ID |
| GET | `/api/orders` | Admin | Get all orders |
| PATCH | `/api/orders/:id/status` | Admin | Update order status |
| PATCH | `/api/orders/:id/cancel` | Customer | Cancel an order |
 
---
 
## 💡 Usage Examples
 
### Register a Customer
```json
POST /api/auth/register
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "123456",
  "role": "customer"
}
```
 
### Register an Admin
```json
POST /api/auth/register
{
  "name": "Admin User",
  "email": "admin@example.com",
  "password": "123456",
  "role": "admin"
}
```
 
### Create a Category (Admin)
```json
POST /api/categories
Authorization: Bearer <admin_token>
{
  "name": "Electronics",
  "description": "Electronic products"
}
```
 
### Create a Product (Admin)
```json
POST /api/products
Authorization: Bearer <admin_token>
{
  "name": "iPhone 15",
  "description": "Latest iPhone",
  "price": 999.99,
  "stock": 10,
  "categoryId": 1
}
```
 
### Add to Cart (Customer)
```json
POST /api/cart
Authorization: Bearer <customer_token>
{
  "productId": 1,
  "quantity": 2
}
```
 
### Place Order from Cart (Customer)
```json
POST /api/orders
Authorization: Bearer <customer_token>
{}
```
 
### Place Order with Specific Items (Customer)
```json
POST /api/orders
Authorization: Bearer <customer_token>
{
  "items": [
    { "productId": 1, "quantity": 2 },
    { "productId": 2, "quantity": 1 }
  ]
}
```
 
### Update Order Status (Admin)
```json
PATCH /api/orders/1/status
Authorization: Bearer <admin_token>
{
  "status": "shipped"
}
```
 
---
 
## 🗄️ Database Entities
 
### User
| Field | Type | Description |
|-------|------|-------------|
| id | int | Primary key |
| name | varchar | Full name |
| email | varchar | Unique email |
| password | varchar | Hashed password |
| role | enum | admin / customer |
| cancellationCount | int | Tracks cancellations |
| isFlagged | boolean | Fraud flag |
 
### Product
| Field | Type | Description |
|-------|------|-------------|
| id | int | Primary key |
| name | varchar | Product name |
| description | varchar | Description |
| price | decimal | Product price |
| stock | int | Available stock |
| image | varchar | Image URL |
| isActive | boolean | Active status |
| category | relation | ManyToOne → Category |
 
### Order
| Field | Type | Description |
|-------|------|-------------|
| id | int | Primary key |
| user | relation | ManyToOne → User |
| items | relation | OneToMany → OrderItem |
| total | decimal | Calculated total |
| status | enum | pending / shipped / delivered / cancelled |
 
### OrderItem
| Field | Type | Description |
|-------|------|-------------|
| id | int | Primary key |
| order | relation | ManyToOne → Order |
| product | relation | ManyToOne → Product |
| quantity | int | Quantity ordered |
| price | decimal | Price at time of order |
 
---
 
## 🔒 Business Rules
 
- Customers **cannot order more** than available stock
- Order total is **always calculated on the backend**
- Stock is **deducted only after** successful order placement
- **Negative inventory is prevented** at all times
- Orders can only be cancelled when status is **Pending**
- Stock is **restored automatically** when an order is cancelled
- Users who cancel **3 or more orders** are flagged for fraud and blocked from further cancellations
- Database **transactions** ensure data consistency across all order operations
 
---
 
## 👥 Roles & Permissions
 
| Feature | Admin | Customer |
|---------|-------|----------|
| Register / Login | ✅ | ✅ |
| View Products | ✅ | ✅ |
| Manage Products | ✅ | ❌ |
| Manage Categories | ✅ | ❌ |
| View All Orders | ✅ | ❌ |
| Update Order Status | ✅ | ❌ |
| Use Cart | ❌ | ✅ |
| Place Order | ❌ | ✅ |
| View Own Orders | ❌ | ✅ |
| Cancel Own Order | ❌ | ✅ |
 
---
 
## 🛡️ Security
 
- Passwords are hashed using **bcryptjs**
- JWT tokens expire after **7 days**
- All protected routes require a valid JWT token
- Role-based guards prevent unauthorized access
- Input validation on all endpoints
 
---
 

## 👨 Author

Mirza Salem  
[GitHub](https://github.com/mirzasalem/) | [LinkedIn](https://www.linkedin.com/in/mirzasalem/) | [Portfolio](https://mirzasalem.vercel.app/)

