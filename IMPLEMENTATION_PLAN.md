# MERN Stack Project Implementation Plan

## 1. Project Analysis
The updated analysis of the existing codebase confirms 'Shri_design' is an E-commerce application with two main user roles: **Customer** and **Admin**.
-   **Frontend**: Built with Vite + React + TypeScript + Tailwind CSS + Shadcn UI.
-   **Current State**: Visual UI is complete but uses hardcoded/mock data.
-   **Goal**: Replace mock data with a real MERN backend.

## 2. Architecture Overview
We will implement a standard MERN stack architecture.
-   **Client**: The existing React app (will need refactoring to fetch data).
-   **Server**: Node.js + Express (serving the API).
-   **Database**: MongoDB (storing Users, Products, Orders, Carts).

## 3. Database Schema
We will use Mongoose for Object Data Modeling (ODM).

### 3.1 User
-   `name`: String
-   `email`: String (Unique, Indexed)
-   `password`: String (Hashed)
-   `role`: String (Enum: 'admin', 'customer')
-   `address`: String (Optional)
-   `phone`: String (Optional)

### 3.2 Product
-   `name`: String
-   `description`: String
-   `price`: Number
-   `category`: String
-   `stock`: Number
-   `sku`: String
-   `images`: [String] (URLs)
-   `isNewArrival`: Boolean (Default: false)

### 3.3 Cart
-   `userId`: ObjectId (Ref: User)
-   `items`: [
    -   `productId`: ObjectId (Ref: Product)
    -   `quantity`: Number
    ]

### 3.4 Order
-   `userId`: ObjectId (Ref: User)
-   `items`: [
    -   `productId`: ObjectId (Ref: Product)
    -   `name`: String (Snapshot)
    -   `price`: Number (Snapshot)
    -   `quantity`: Number
    ]
-   `totalAmount`: Number
-   `status`: String (Enum: 'Pending', 'Processing', 'Shipped', 'Delivered', 'Cancelled')
-   `paymentStatus`: String (Enum: 'Pending', 'Paid', 'Failed')
-   `shippingAddress`: String

## 4. API Endpoints

### Auth
-   `POST /api/auth/register` - Register new user
-   `POST /api/auth/login` - Login user (returns JWT)
-   `GET /api/auth/me` - Get current user profile

### Products
-   `GET /api/products` - List all products (with filters)
-   `GET /api/products/:id` - Get single product
-   `POST /api/products` - Create product (Admin only)
-   `PUT /api/products/:id` - Update product (Admin only)
-   `DELETE /api/products/:id` - Delete product (Admin only)

### Cart
-   `GET /api/cart` - Get user's cart
-   `POST /api/cart` - Add item to cart
-   `PUT /api/cart/:productId` - Update item quantity
-   `DELETE /api/cart/:productId` - Remove item from cart

### Orders
-   `POST /api/orders` - Create new order
-   `GET /api/orders` - Get all orders (Admin) / My orders (Customer)
-   `GET /api/orders/:id` - Get order details
-   `PATCH /api/orders/:id/status` - Update order status (Admin)

## 5. Execution Steps

### Phase 1: Backend Setup
1.  Initialize `server` folder.
2.  Install `express`, `mongoose`, `dotenv`, `cors`, `bcryptjs`, `jsonwebtoken`.
3.  Create connection to MongoDB.
4.  Setup basic server entry point (`index.js`).

### Phase 2: Core Implementation
1.  Create Mongoose Models (`models/User.js`, `models/Product.js`, etc.).
2.  Create Controllers for Auth, Products, and Orders.
3.  Setup Routes (`routes/authRoutes.js`, `routes/productRoutes.js`, etc.).
4.  Implement Middleware (`authMiddleware`, `adminMiddleware`).

### Phase 3: Frontend Integration
1.  Configure API client (Axios or Fetch wrapper).
2.  **Auth Integration**: Connect Login/Register pages to API.
3.  **Products Integration**: Replace hardcoded product lists in `Shop`, `Products` (Admin), and `ProductDetail` with API data using React Query.
4.  **Cart & Checkout**: Connect Cart page to Cart API; Checkout processes the Order.
5.  **Dashboard**: Connect Admin Dashboard to real analytics endpoints.

## 6. Next Actions
-   [ ] Create `server` directory and initialize project.
-   [ ] Define MongoDB connection string (Env var).
-   [ ] Begin Phase 1 & 2 implementation.
