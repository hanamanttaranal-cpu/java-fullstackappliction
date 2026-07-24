

https://github.com/user-attachments/assets/c8526f5b-2ffd-4bb6-8950-c83f4acdd819










# 🛒 ShopNow - Java Full Stack E-Commerce Application

A complete, production-ready e-commerce application built with **Spring Boot** (backend) and **React** (frontend).

---

## 📁 Project Structure

```
ecommerce/
├── backend/                          # Spring Boot REST API
│   ├── src/main/java/com/ecommerce/
│   │   ├── EcommerceApplication.java       # Main entry point
│   │   ├── config/
│   │   │   ├── SecurityConfig.java         # JWT & CORS security
│   │   │   └── AppConfig.java              # Beans: ModelMapper, Stripe, Cloudinary
│   │   ├── controller/
│   │   │   ├── AuthController.java         # POST /auth/register, /auth/login
│   │   │   ├── ProductController.java      # CRUD /products
│   │   │   ├── CartController.java         # GET/POST/PUT/DELETE /cart
│   │   │   ├── OrderController.java        # POST/GET /orders
│   │   │   └── AdminController.java        # GET /admin/dashboard
│   │   ├── service/
│   │   │   ├── AuthService.java            # Register, Login logic
│   │   │   ├── ProductService.java         # Product CRUD + search
│   │   │   ├── CartService.java            # Cart management
│   │   │   └── OrderService.java           # Order placement
│   │   ├── model/
│   │   │   ├── User.java                   # User entity (roles: ADMIN, CUSTOMER)
│   │   │   ├── Product.java                # Product with images, reviews, tags
│   │   │   ├── Category.java               # Hierarchical categories
│   │   │   ├── Cart.java + CartItem.java   # Shopping cart
│   │   │   ├── Order.java + OrderItem.java # Order with statuses
│   │   │   ├── Address.java                # Shipping address
│   │   │   ├── Review.java                 # Product reviews & ratings
│   │   │   ├── Coupon.java                 # Discount coupons
│   │   │   └── ProductImage.java           # Product image (Cloudinary)
│   │   ├── repository/
│   │   │   ├── UserRepository.java
│   │   │   ├── ProductRepository.java      # Custom search queries
│   │   │   ├── OrderRepository.java        # Revenue/count queries
│   │   │   ├── CategoryRepository.java
│   │   │   ├── CartRepository.java
│   │   │   ├── ReviewRepository.java
│   │   │   └── CouponRepository.java
│   │   ├── dto/
│   │   │   ├── AuthRequest/Response.java   # Login/Register payloads
│   │   │   ├── RegisterRequest.java
│   │   │   ├── UserDTO.java
│   │   │   ├── ProductDTO.java + ProductRequest.java
│   │   │   ├── OrderDTO.java + OrderItemDTO.java
│   │   │   ├── CartDTO.java + CartItemDTO.java
│   │   │   ├── AddressDTO.java
│   │   │   └── ApiResponse.java            # Generic API wrapper
│   │   ├── security/
│   │   │   ├── JwtUtils.java               # Token generation & validation
│   │   │   ├── JwtAuthenticationFilter.java # Request interceptor
│   │   │   └── UserDetailsServiceImpl.java  # Spring Security integration
│   │   └── exception/
│   │       ├── GlobalExceptionHandler.java  # @RestControllerAdvice
│   │       ├── ResourceNotFoundException.java
│   │       ├── BadRequestException.java
│   │       └── UnauthorizedException.java
│   ├── src/main/resources/
│   │   └── application.properties          # DB, JWT, Mail, Stripe, Cloudinary config
│   └── pom.xml                             # Maven dependencies
│
└── frontend/                         # React Application
    ├── public/
    │   └── index.html
    ├── src/
    │   ├── index.js                        # React DOM entry
    │   ├── App.jsx                         # Router + Provider setup
    │   ├── store/
    │   │   ├── index.js                    # Redux + redux-persist store
    │   │   ├── authSlice.js                # Login/Register/Logout state
    │   │   ├── cartSlice.js                # Cart state (fetch/add/update/remove)
    │   │   └── productSlice.js             # Products state (list/search/featured)
    │   ├── components/
    │   │   ├── common/
    │   │   │   ├── Navbar.jsx              # Responsive navbar with cart badge
    │   │   │   ├── Footer.jsx              # Footer with links
    │   │   │   └── index.js                # LoadingSpinner, StarRating, Pagination
    │   │   ├── product/
    │   │   │   ├── ProductCard.jsx         # Card with Add-to-Cart
    │   │   │   └── ProductFilter.jsx       # Category/price/sort filters
    │   │   └── cart/
    │   │       └── CartItem.jsx            # Cart item with qty controls
    │   ├── pages/
    │   │   ├── HomePage.jsx                # Hero, categories, featured products
    │   │   ├── ProductsPage.jsx            # Grid + sidebar filter + search
    │   │   ├── ProductDetailPage.jsx       # Gallery, price, add-to-cart
    │   │   ├── CartPage.jsx                # Cart with order summary
    │   │   ├── LoginPage.jsx               # Login form
    │   │   ├── RegisterPage.jsx            # Registration form
    │   │   ├── OrdersPage.jsx              # Order history
    │   │   └── AdminDashboard.jsx          # Admin stats & quick actions
    │   ├── utils/
    │   │   └── axios.js                    # Axios instance with JWT interceptors
    │   └── styles/
    │       └── global.css                  # Complete responsive CSS design system
    └── package.json
```

---

## 🚀 Tech Stack

### Backend
| Technology | Purpose |
|---|---|
| Spring Boot 3.2 | REST API framework |
| Spring Security + JWT | Authentication & authorization |
| Spring Data JPA + Hibernate | ORM & database access |
| MySQL | Primary database |
| Stripe | Payment processing |
| Cloudinary | Image upload & storage |
| Lombok | Boilerplate reduction |
| ModelMapper | DTO mapping |
| Springdoc OpenAPI | API documentation (Swagger) |

### Frontend
| Technology | Purpose |
|---|---|
| React 18 | UI library |
| Redux Toolkit + redux-persist | State management |
| React Router v6 | Client-side routing |
| Axios | HTTP client with interceptors |
| React Hot Toast | Notifications |
| React Icons | Icon library |
| Framer Motion | Animations |

---

## ⚙️ Setup & Installation

### Prerequisites
- Java 17+
- Maven 3.8+
- Node.js 18+
- MySQL 8.0+

---

### 1. Database Setup

```sql
CREATE DATABASE ecommerce_db;
CREATE USER 'ecomm_user'@'localhost' IDENTIFIED BY 'yourpassword';
GRANT ALL PRIVILEGES ON ecommerce_db.* TO 'ecomm_user'@'localhost';
FLUSH PRIVILEGES;
```

---

### 2. Backend Setup

```bash
cd backend

# Edit src/main/resources/application.properties
# Update: DB credentials, JWT secret, Stripe key, Cloudinary credentials

# Build and run
mvn clean install
mvn spring-boot:run
```

Backend starts at: **http://localhost:8080/api**
Swagger UI: **http://localhost:8080/api/swagger-ui.html**

---

### 3. Frontend Setup

```bash
cd frontend

# Install dependencies
npm install

# Create .env file
echo "REACT_APP_API_URL=http://localhost:8080/api" > .env

# Start development server
npm start
```

Frontend starts at: **http://localhost:3000**

---

## 🔑 Environment Variables

### Backend (`application.properties`)
```properties
# Required - update these:
spring.datasource.url=jdbc:mysql://localhost:3306/ecommerce_db
spring.datasource.username=root
spring.datasource.password=YOUR_DB_PASSWORD

app.jwt.secret=YOUR_256_BIT_SECRET_KEY_HERE_MINIMUM_32_CHARS
stripe.api.key=sk_test_YOUR_STRIPE_KEY
cloudinary.cloud-name=YOUR_CLOUD_NAME
cloudinary.api-key=YOUR_API_KEY
cloudinary.api-secret=YOUR_API_SECRET
```

### Frontend (`.env`)
```env
REACT_APP_API_URL=http://localhost:8080/api
REACT_APP_STRIPE_PUBLIC_KEY=pk_test_YOUR_STRIPE_PUBLIC_KEY
```

---

## 📡 API Endpoints

### Authentication
```
POST   /api/auth/register      Register new user
POST   /api/auth/login         Login, returns JWT tokens
```

### Products
```
GET    /api/products            List products (paginated)
GET    /api/products/{id}       Get product by ID
GET    /api/products/search     Search with filters
GET    /api/products/featured   Get featured products
POST   /api/products            Create product (ADMIN)
PUT    /api/products/{id}       Update product (ADMIN)
DELETE /api/products/{id}       Delete product (ADMIN)
```

### Cart
```
GET    /api/cart                Get current user's cart
POST   /api/cart/add            Add item to cart
PUT    /api/cart/item/{id}      Update item quantity
DELETE /api/cart/item/{id}      Remove item from cart
DELETE /api/cart/clear          Clear entire cart
```

### Orders
```
POST   /api/orders              Place an order
GET    /api/orders              Get user's orders
GET    /api/orders/{id}         Get order details
PUT    /api/orders/{id}/status  Update order status (ADMIN)
```

### Admin
```
GET    /api/admin/dashboard     Get dashboard stats (ADMIN)
GET    /api/admin/users         List all users (ADMIN)
```

---

## 🗃️ Database Schema (Key Tables)

```
users           → id, email, password, firstName, lastName, role, phone
products        → id, name, price, discountPrice, stockQuantity, categoryId, brand, featured
categories      → id, name, slug, parentId, active
product_images  → id, productId, imageUrl, isPrimary
cart            → id, userId
cart_items      → id, cartId, productId, quantity
orders          → id, orderNumber, userId, status, paymentStatus, totalAmount
order_items     → id, orderId, productId, quantity, price
reviews         → id, productId, userId, rating, comment
addresses       → id, userId, addressLine1, city, state, postalCode, country
coupons         → id, code, discountType, discountValue, usageLimit
```

---

## 🔐 Security Features

- **JWT Authentication** — access + refresh tokens
- **Role-based Authorization** — ADMIN, CUSTOMER roles via Spring Security
- **Password Encryption** — BCrypt hashing
- **CORS Configuration** — Restricted to allowed origins
- **Input Validation** — Jakarta Bean Validation on all DTOs
- **Global Exception Handling** — Consistent error response format

---

## 🎨 Frontend Features

- **Responsive Design** — Mobile-first CSS, works on all screen sizes
- **Redux Persist** — Cart and auth state survive page refresh
- **JWT Interceptor** — Automatically attaches token to all API requests
- **Toast Notifications** — Success/error feedback for user actions
- **Protected Routes** — Redirect unauthenticated users to login
- **Search & Filter** — Real-time product search with category/price filters
- **Optimistic UI** — Instant cart updates with error rollback

---

## 🛠️ Extending the Project

### Add a new feature (e.g., Wishlist):
1. Create `Wishlist.java` model in `/model`
2. Create `WishlistRepository.java` in `/repository`
3. Create `WishlistService.java` in `/service`
4. Create `WishlistController.java` in `/controller`
5. Add `wishlistSlice.js` to Redux store
6. Create the React component/page

### Add Payment (Stripe):
1. Create a `/payments/create-intent` endpoint in backend
2. Return `client_secret` from Stripe
3. Use `@stripe/react-stripe-js` `CardElement` in frontend
4. Confirm payment and create order on success

---

## 📦 Build for Production

### Backend
```bash
cd backend
mvn clean package -DskipTests
java -jar target/ecommerce-backend-1.0.0.jar
```

### Frontend
```bash
cd frontend
npm run build
# Serves the /build folder via any static file server
```

---

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Commit changes: `git commit -m "Add your feature"`
4. Push: `git push origin feature/your-feature`
5. Open a Pull Request

---

## 📄 License

#####MIT License — free to use for personal and commercial projects.
