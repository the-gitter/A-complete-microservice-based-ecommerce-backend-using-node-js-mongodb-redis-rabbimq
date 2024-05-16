# The Gitter

### 1. User Microservice

**Responsibilities:**

- User authentication and registration.
- Managing user profiles.
- Handling user roles (e.g., admin, customer).

**Key Technologies:**

- Firebase Admin SDK for authentication.
- Firestore for storing user profile data.
- Express.js for API handling.

**Endpoints:** for testing

- for every route use prefix '/api/[{route-name}]
- `Route names are : [ firebase-singup , firebase-login,refresh-tokens , logout]`

**Endpoints:** after deployment

- `POST /auth/firebase-singup`: Register a new user.
- `POST /auth/firebase-login`: Authenticate a user and issue a JWT.
- `POST /auth/refresh-tokens`: to get new set of tokens
- `POST /auth/logout`: to logout out / invalidates tokens

**`not ye implemented`**

- `GET /users/profile`: Retrieve the user's profile.
- `PUT /users/profile`: Update the user's profile.
- `GET /users`: Retrieve a list of users (admin only).
- `GET /users/:id`: Retrieve a specific user by ID (admin only).
- `PUT /users/:id`: Update a specific user by ID (admin only).
- `DELETE /users/:id`: Delete a user by ID (admin only).

**Architecture:**

```plaintext
User Microservice
src
│   expressApp.ts
│   server.ts
│
├───config
│       firebaseSdkConfig.ts
│       servicesAccountKey.json
│
├───interfaces
├───middlewares
│       firebaseMiddleware.ts
│       multer.js
│
├───models
│       addressModel.ts
│       userModel.ts
│
├───repositories
│       authRepository.ts
│       cloudinary-repository.ts
│       userRepository.ts
│
├───routes
│       authRoutes.ts
│
├───services
│       authService.ts
│
├───types
└───utils
    │   generate_keys.ts
    │   init_mongodb.ts
    │   init_redis.ts
    │   jwt_helper.ts
    │   SendApiResponse.ts
    │
    ├───errors
    │       app-errors.ts
    │
    ├───message_broker
    │       message_broker.ts
    │
    └───validators
            handlers.ts
            validators.ts
```

### 2. Catalog Microservice

**Responsibilities:**

- Managing product information (audio equipment).
- Handling product categories.
- Maintaining stock levels.
- Managing product reviews and ratings.

**Key Technologies:**

- MongoDB for product and category data.
- Express.js for API handling.

**Endpoints:**

- `POST /products`: Create a new product.
- `GET /products`: Retrieve a list of products.
- `GET /products/:id`: Retrieve a product by ID.
- `PUT /products/:id`: Update a product by ID.
- `DELETE /products/:id`: Delete a product by ID.
- `POST /categories`: Create a new category.
- `GET /categories`: Retrieve a list of categories.
- `PUT /stock/:productId`: Update stock levels for a product.
- `POST /products/:id/reviews`: Add a review for a product.
- `GET /products/:id/reviews`: Retrieve reviews for a product.
- `DELETE /products/:id/reviews/:reviewId`: Delete a review (admin only).

**Architecture:**

```plaintext
Catalog Microservice
├── controllers
│   ├── productController.js
│   ├── categoryController.js
│   └── reviewController.js
├── models
│   ├── productModel.js
│   ├── categoryModel.js
│   └── reviewModel.js
├── routes
│   ├── productRoutes.js
│   ├── categoryRoutes.js
│   └── reviewRoutes.js
├── services
│   └── stockService.js
├── middlewares
│   └── authMiddleware.js
├── app.js
└── config.js
```

### 3. Order Microservice

**Responsibilities:**

- Creating and managing orders.
- Handling order items.
- Updating order status.
- Managing order history.

**Key Technologies:**

- PostgreSQL for storing order data.
- Express.js for API handling.

**Endpoints:**

- `POST /orders`: Create a new order.
- `GET /orders`: Retrieve a list of orders (customer-specific).
- `GET /orders/:id`: Retrieve an order by ID.
- `PUT /orders/:id`: Update an order by ID.
- `DELETE /orders/:id`: Cancel an order.
- `POST /order-items`: Add items to an order.
- `GET /order-items/:orderId`: Retrieve items for a specific order.

**Architecture:**

```plaintext
Order Microservice
├── controllers
│   ├── orderController.js
│   └── orderItemController.js
├── models
│   ├── orderModel.js
│   └── orderItemModel.js
├── routes
│   ├── orderRoutes.js
│   └── orderItemRoutes.js
├── services
│   └── orderService.js
├── middlewares
│   └── authMiddleware.js
├── app.js
└── config.js
```

### 4. Payment Microservice

**Responsibilities:**

- Processing payments.
- Managing transactions.
- Recording payment details.
- Handling refunds.

**Key Technologies:**

- Stripe SDK (or any payment gateway) for payment processing.
- MongoDB for storing transaction data.
- Express.js for API handling.

**Endpoints:**

- `POST /payments`: Process a payment.
- `GET /payments/:orderId`: Retrieve payment details for an order.
- `POST /payments/:orderId/refund`: Process a refund for an order.
- `GET /transactions`: Retrieve a list of transactions.

**Architecture:**

```plaintext
Payment Microservice
├── controllers
│   ├── paymentController.js
│   └── transactionController.js
├── models
│   └── transactionModel.js
├── routes
│   ├── paymentRoutes.js
│   └── transactionRoutes.js
├── services
│   └── paymentService.js
├── middlewares
│   └── authMiddleware.js
├── app.js
└── config.js
```

### 5. Inventory Microservice

**Responsibilities:**

- Managing stock levels.
- Syncing stock information with the Catalog Microservice.
- Handling inventory adjustments.

**Key Technologies:**

- MongoDB for inventory data.
- Express.js for API handling.

**Endpoints:**

- `GET /inventory`: Retrieve all inventory items.
- `GET /inventory/:productId`: Retrieve inventory details for a product.
- `PUT /inventory/:productId`: Update inventory for a product.
- `POST /inventory/adjustment`: Adjust inventory levels (e.g., after a sale or return).

**Architecture:**

```plaintext
Inventory Microservice
├── controllers
│   └── inventoryController.js
├── models
│   └── inventoryModel.js
├── routes
│   └── inventoryRoutes.js
├── services
│   └── inventoryService.js
├── middlewares
│   └── authMiddleware.js
├── app.js
└── config.js
```

### 6. Notification Microservice

**Responsibilities:**

- Sending email and SMS notifications.
- Managing notification templates.
- Handling event-driven notifications (e.g., order confirmations, shipment updates).

**Key Technologies:**

- NodeMailer or any email service for sending emails.
- Twilio or any SMS service for sending SMS.
- MongoDB for storing notification templates and logs.
- Express.js for API handling.

**Endpoints:**

- `POST /notifications/email`: Send an email notification.
- `POST /notifications/sms`: Send an SMS notification.
- `GET /notifications/templates`: Retrieve notification templates.
- `POST /notifications/templates`: Create a new notification template.
- `PUT /notifications/templates/:id`: Update a notification template by ID.
- `DELETE /notifications/templates/:id`: Delete a notification template by ID.

**Architecture:**

```plaintext
Notification Microservice
├── controllers
│   ├── emailController.js
│   └── smsController.js
├── models
│   └── templateModel.js
├── routes
│   ├── emailRoutes.js
│   ├── smsRoutes.js
│   └── templateRoutes.js
├── services
│   ├── emailService.js
│   └── smsService.js
├── middlewares
│   └── authMiddleware.js
├── app.js
└── config.js
```

### 7. API Gateway

**Responsibilities:**

- Routing requests to appropriate microservices.
- Handling cross-cutting concerns (authentication, rate limiting, logging).
- Providing a unified entry point for clients.

**Key Technologies:**

- Kong, NGINX, or AWS API Gateway.

**Endpoints Configuration Example:**

```plaintext
API Gateway
├── kong.yml
```

- Example `kong.yml` configuration:

```yaml
_format_version: "2.1"
services:
  - name: user-service
    url: http://user-service:3000
    routes:
      - name: user-routes
        paths:
          - /users

  - name: catalog-service
    url: http://catalog-service:3000
    routes:
      - name: catalog-routes
        paths:
          - /products
          - /categories

  - name: order-service
    url: http://order-service:3000
    routes:
      - name: order-routes
        paths:
          - /orders
          - /order-items

  - name: payment-service
    url: http://payment-service:3000
    routes:
      - name: payment-routes
        paths:
          - /payments
          - /transactions

  - name: inventory-service
    url: http://inventory-service:3000
    routes:
      - name: inventory-routes
        paths:
          - /inventory

  - name: notification-service
    url: http://notification-service:3000
    routes:
      - name: notification-routes
        paths:
          - /notifications
```

### Summary of Responsibilities and Endpoints:

\*\*User Microservice

:\*\*

- **Features:**
  - User registration, login, profile management, and user role management.
- **Endpoints:**
  - `POST /users/register`
  - `POST /users/login`
  - `GET /users/profile`
  - `PUT /users/profile`
  - `GET /users`
  - `GET /users/:id`
  - `PUT /users/:id`
  - `DELETE /users/:id`

**Catalog Microservice:**

- **Features:**
  - Product and category management, stock updates, and product reviews.
- **Endpoints:**
  - `POST /products`
  - `GET /products`
  - `GET /products/:id`
  - `PUT /products/:id`
  - `DELETE /products/:id`
  - `POST /categories`
  - `GET /categories`
  - `PUT /stock/:productId`
  - `POST /products/:id/reviews`
  - `GET /products/:id/reviews`
  - `DELETE /products/:id/reviews/:reviewId`

**Order Microservice:**

- **Features:**
  - Order creation, item management, status updates, and order history.
- **Endpoints:**
  - `POST /orders`
  - `GET /orders`
  - `GET /orders/:id`
  - `PUT /orders/:id`
  - `DELETE /orders/:id`
  - `POST /order-items`
  - `GET /order-items/:orderId`

**Payment Microservice:**

- **Features:**
  - Payment processing, transaction management, and handling refunds.
- **Endpoints:**
  - `POST /payments`
  - `GET /payments/:orderId`
  - `POST /payments/:orderId/refund`
  - `GET /transactions`

**Inventory Microservice:**

- **Features:**
  - Managing and syncing stock levels, inventory adjustments.
- **Endpoints:**
  - `GET /inventory`
  - `GET /inventory/:productId`
  - `PUT /inventory/:productId`
  - `POST /inventory/adjustment`

**Notification Microservice:**

- **Features:**
  - Sending email and SMS notifications, managing notification templates.
- **Endpoints:**
  - `POST /notifications/email`
  - `POST /notifications/sms`
  - `GET /notifications/templates`
  - `POST /notifications/templates`
  - `PUT /notifications/templates/:id`
  - `DELETE /notifications/templates/:id`
