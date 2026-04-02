# 🎬 Netflix REST API

A fully-featured REST API for a Netflix-like streaming platform, built with Node.js, Express.js, and MongoDB. This project demonstrates production-ready backend development practices including authentication, authorization, image handling, and comprehensive API endpoints.

---

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Key Features](#key-features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Installation & Setup](#installation--setup)
- [API Endpoints](#api-endpoints)
- [Environment Configuration](#environment-configuration)
- [Running the Project](#running-the-project)
- [Code Quality & Best Practices](#code-quality--best-practices)
- [Future Enhancements](#future-enhancements)

---

## 🎯 Project Overview

Netflix REST API is a comprehensive backend solution for a streaming platform that handles:
- **User Management**: Registration, authentication, and profile management
- **Movie Catalog**: Browse, search, and retrieve movie details
- **Subscription Plans**: Multiple subscription tiers with different features
- **Admin Panel**: Administrative controls for managing content and users
- **Media Management**: Image upload and storage functionality

This project is designed to be scalable, secure, and maintainable with proper separation of concerns.

---

## ✨ Key Features

### Authentication & Security
- **JWT-based Authentication**: Secure token generation and validation
- **Password Encryption**: bcrypt for secure password hashing
- **Role-based Access Control**: Separate authentication for users and admins
- **CORS Support**: Cross-Origin Resource Sharing enabled for frontend integration
- **Security Headers**: Helmet.js for HTTP security headers
- **Request Logging**: Morgan middleware for monitoring and debugging

### User Management
- User registration and login
- User profile management
- Authentication token generation and verification
- Subscription plan assignment

### Movie Management
- Create, retrieve, and manage movies
- Movie details and metadata
- Image upload for posters and thumbnails
- Category and genre support

### Subscription Plans
- Multiple subscription tier management
- Plan pricing and features
- User subscription assignment

### Admin Features
- Administrative user management
- Content management capabilities
- User analytics and control
- Dedicated admin authentication

### File Handling
- Image upload functionality
- File storage and management
- Multer integration for multipart/form-data handling

---

## 🛠 Tech Stack

| Category | Technology | Purpose |
|----------|-----------|---------|
| **Runtime** | Node.js | JavaScript runtime environment |
| **Framework** | Express.js 4.18.1 | Web application framework |
| **Database** | MongoDB 4.5.0 | NoSQL database |
| **ODM** | Mongoose 6.3.1 | MongoDB object modeling |
| **Authentication** | JWT (jsonwebtoken 8.5.1) | Token-based authentication |
| **Security** | bcrypt 5.0.1 | Password hashing |
| **Security Headers** | Helmet 5.0.2 | HTTP security headers |
| **File Upload** | Multer 1.4.4 | Multipart form data handling |
| **CORS** | cors 2.8.5 | Cross-origin resource sharing |
| **Logging** | Morgan 1.10.0 | HTTP request logging |
| **Environment** | dotenv 16.0.1 | Environment variable management |
| **Utilities** | moment 2.29.3 | Date and time handling |

---

## 📁 Project Structure

```
Netflix-rest-api/
├── app/
│   ├── config/
│   │   └── config.js              # Database configuration
│   ├── controllers/
│   │   ├── admin.controller.js     # Admin business logic
│   │   ├── user.controller.js      # User business logic
│   │   ├── movie.controller.js     # Movie business logic
│   │   ├── movieDetail.controller.js # Movie details logic
│   │   └── subscriptionPlan.controller.js # Subscription logic
│   ├── models/
│   │   ├── admin.modal.js          # Admin schema
│   │   ├── user.modal.js           # User schema
│   │   ├── movie.modal.js          # Movie schema
│   │   ├── movieDetail.modal.js    # Movie detail schema
│   │   └── subscriptionPlan.modal.js # Subscription schema
│   ├── middleware/
│   │   ├── async.js                # Async error handling
│   │   ├── authToken.js            # User authentication
│   │   ├── authTokenForAdmin.js    # Admin authentication
│   │   ├── generateToken.js        # JWT token generation
│   │   └── uploadImage.js          # Image upload handling
│   ├── routes/
│   │   ├── admin.route.js          # Admin endpoints
│   │   ├── user.route.js           # User endpoints
│   │   ├── movie.route.js          # Movie endpoints
│   │   ├── movieDetail.route.js    # Movie detail endpoints
│   │   └── subscriptionPlan.route.js # Subscription endpoints
├── uploads/
│   └── images/                     # User-uploaded images
├── package.json                    # Project dependencies
├── server.js                       # Application entry point
├── .env                            # Environment variables (not in repo)
├── .gitignore                      # Git ignore patterns
└── README.md                       # This file
```

---

## 🚀 Installation & Setup

### Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** (v14.0.0 or higher) - [Download](https://nodejs.org/)
- **npm** (v6.0.0 or higher) - Comes with Node.js
- **MongoDB** (v4.0 or higher) - [Download](https://www.mongodb.com/try/download/community)
- **Git** - [Download](https://git-scm.com/)

### Step 1: Clone the Repository

```bash
git clone https://github.com/yourusername/Netflix-rest-api.git
cd Netflix-rest-api
```

### Step 2: Install Dependencies

```bash
npm install
```

This will install all required packages listed in `package.json`:
- Express.js (web framework)
- Mongoose (database ODM)
- JWT (authentication)
- bcrypt (password security)
- And other supporting libraries

### Step 3: Configure Environment Variables

Create a `.env` file in the project root directory:

```bash
cp .env.example .env  # (if example exists)
# Or manually create .env file
```

Add the following environment variables:

```env
# Server Configuration
PORT=5000
NODE_ENV=development

# Database Configuration
MONGO_URI=mongodb://localhost:27017/netflix-clone
# For MongoDB Atlas:
# MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/netflix-clone

# JWT Configuration
JWT_SECRET=your_jwt_secret_key_here
JWT_EXPIRE=7d

# CORS Configuration (Frontend URL)
CORS_ORIGIN=http://localhost:3000

# Image Upload
MAX_FILE_SIZE=5242880  # 5MB in bytes
UPLOAD_PATH=./uploads/images
```

### Step 4: Start MongoDB

**For Local MongoDB:**
```bash
# Windows
mongod

# macOS
brew services start mongodb-community

# Linux
sudo systemctl start mongod
```

**For MongoDB Atlas (Cloud):**
- Update `MONGO_URI` in `.env` with your connection string

---

## 📡 API Endpoints

### Authentication Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/v1/api/user/register` | Register a new user |
| `POST` | `/v1/api/user/login` | Login user and get JWT token |
| `GET` | `/v1/api/user/profile` | Get user profile (requires auth) |
| `PUT` | `/v1/api/user/update` | Update user profile (requires auth) |
| `POST` | `/v1/api/admin/login` | Admin login |

### Movie Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/v1/api/movies` | Get all movies |
| `GET` | `/v1/api/movies/:id` | Get movie by ID |
| `POST` | `/v1/api/movies` | Create new movie (admin only) |
| `PUT` | `/v1/api/movies/:id` | Update movie (admin only) |
| `DELETE` | `/v1/api/movies/:id` | Delete movie (admin only) |

### Movie Details Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/v1/api/movieDetail` | Get all movie details |
| `GET` | `/v1/api/movieDetail/:id` | Get movie details by ID |
| `POST` | `/v1/api/movieDetail` | Create movie details (admin only) |
| `PUT` | `/v1/api/movieDetail/:id` | Update movie details (admin only) |

### Subscription Plan Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/v1/api/subscription-plan` | Get all subscription plans |
| `GET` | `/v1/api/subscription-plan/:id` | Get plan by ID |
| `POST` | `/v1/api/subscription-plan` | Create plan (admin only) |
| `PUT` | `/v1/api/subscription-plan/:id` | Update plan (admin only) |

### Admin Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/v1/api/admin/users` | Get all users (admin only) |
| `DELETE` | `/v1/api/admin/users/:id` | Delete user (admin only) |
| `POST` | `/v1/api/admin/upload` | Upload image (admin only) |

---

## ⚙️ Environment Configuration

### `.env` File Example

```env
# Server
PORT=5000
NODE_ENV=development

# MongoDB Connection
MONGO_URI=mongodb://localhost:27017/netflix-clone

# JWT Secrets
JWT_SECRET=your-super-secret-jwt-key-change-this-in-production
JWT_EXPIRE=7d

# CORS
CORS_ORIGIN=http://localhost:3000

# File Upload
UPLOAD_PATH=./uploads/images
MAX_FILE_SIZE=5242880

# Logging
LOG_LEVEL=debug
```

### Important Security Notes

- **Never commit `.env` file** to version control
- Use strong, random secret keys in production
- Rotate secrets periodically
- Use environment-specific configurations
- Enable HTTPS in production

---

## 🏃 Running the Project

### Development Mode

```bash
# Install dependencies (first time only)
npm install

# Start MongoDB
mongod  # (or your MongoDB service)

# Run the server
node server.js

# Server will start on http://localhost:5000
```

### Adding npm Scripts (Recommended)

Update `package.json` to add these scripts:

```json
"scripts": {
  "start": "node server.js",
  "dev": "nodemon server.js",
  "test": "jest --passWithNoTests"
}
```

Then run with:
```bash
npm start          # Production
npm run dev        # Development with auto-reload
npm test           # Run tests
```

### Using Nodemon for Development

For automatic server restart on file changes:

```bash
npm install --save-dev nodemon
npm run dev
```

---

## 🔒 Code Quality & Best Practices

### Architecture Patterns

✅ **MVC Pattern with Separation of Concerns**
- Controllers handle business logic
- Models define database schemas
- Routes handle HTTP requests
- Middleware handles cross-cutting concerns

✅ **Middleware Stack**
- CORS for cross-origin requests
- Morgan for HTTP logging
- Helmet for security headers
- Express JSON parser for request parsing
- Custom authentication middleware

✅ **Security Best Practices**
- JWT token-based authentication
- bcrypt password hashing (salt rounds: 10)
- Role-based access control (User vs Admin)
- Input validation and sanitization
- CORS properly configured

✅ **Error Handling**
- Async error wrapper for route handlers
- Centralized error handling middleware
- Proper HTTP status codes

✅ **Code Organization**
- Clear file structure with logical separation
- Reusable middleware components
- Database configuration separated from application logic
- Environment-based configuration

✅ **Database Best Practices**
- Mongoose ODM for schema validation
- Connection pooling via Mongoose
- Proper indexing on frequently queried fields
- Error handling for database operations

---

## 📚 Key Technologies Explained

### Express.js
Lightweight web framework that handles HTTP requests/responses and route management.

### MongoDB & Mongoose
- **MongoDB**: NoSQL database for flexible data storage
- **Mongoose**: Provides schema validation and easier database operations

### JWT (JSON Web Tokens)
- Stateless authentication mechanism
- Secure token exchange between client and server
- Economical for microservice architectures

### bcrypt
Cryptographic hashing algorithm for secure password storage with salt protection.

### Multer
Middleware for handling file uploads (images, documents, etc.)

---

## 🎓 What Impresses Employers

This project demonstrates:

1. **Full-Stack API Development**: Complete REST API with CRUD operations
2. **Security Implementation**: JWT authentication, password hashing, role-based access
3. **Database Design**: MongoDB schema design with Mongoose
4. **Code Organization**: Clean architecture following MVC pattern
5. **Production-Ready Code**: Error handling, logging, security headers
6. **Best Practices**: 
   - Separation of concerns
   - Middleware usage
   - Environment configuration
   - Proper HTTP status codes
7. **Scalability**: Modular structure allows easy feature additions
8. **Documentation**: Clear code comments and API documentation

---

## 🔮 Future Enhancements

Consider adding these features to expand the project:

- [ ] **Unit & Integration Tests**: Jest/Mocha test suites
- [ ] **API Documentation**: Swagger/OpenAPI specifications
- [ ] **Email Notifications**: User notifications and password reset
- [ ] **Payment Integration**: Stripe/PayPal for subscriptions
- [ ] **Search & Filter**: Advanced movie search capabilities
- [ ] **Pagination**: Implement pagination for large datasets
- [ ] **Caching**: Redis for performance optimization
- [ ] **Rate Limiting**: Prevent abuse with rate limiting middleware
- [ ] **Logging Service**: Winston or similar for better logging
- [ ] **Docker Support**: Containerize the application
- [ ] **CI/CD Pipeline**: Automated testing and deployment
- [ ] **API Versioning**: Backward compatibility management
- [ ] **WebSocket Support**: Real-time features
- [ ] **Analytics**: Track user behavior and engagement

---

## 📝 API Request Examples

### Register User
```bash
curl -X POST http://localhost:5000/v1/api/user/register \
  -H "Content-Type: application/json" \
  -d '{
    "username": "john_doe",
    "email": "john@example.com",
    "password": "secure_password_123"
  }'
```

### Login User
```bash
curl -X POST http://localhost:5000/v1/api/user/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "john@example.com",
    "password": "secure_password_123"
  }'
```

### Get All Movies (Authenticated)
```bash
curl -X GET http://localhost:5000/v1/api/movies \
  -H "Authorization: Bearer YOUR_JWT_TOKEN"
```

### Upload Image (Admin)
```bash
curl -X POST http://localhost:5000/v1/api/admin/upload \
  -H "Authorization: Bearer ADMIN_JWT_TOKEN" \
  -F "image=@/path/to/image.jpg"
```

---

## 🐛 Troubleshooting

### MongoDB Connection Error
- Ensure MongoDB is running locally or update `MONGO_URI` with your Atlas connection
- Check username and password in connection string
- Verify network access in MongoDB Atlas (IP whitelist)

### JWT Token Errors
- Ensure `JWT_SECRET` matches between token generation and verification
- Check token expiration in your `.env` file
- Verify Authorization header format: `Bearer <token>`

### Port Already in Use
```bash
# Find process using port 5000
lsof -i :5000

# Kill the process
kill -9 <PID>
```

### Image Upload Issues
- Create `uploads/images` directory if it doesn't exist
- Check file size limits in `uploadImage.js` middleware
- Verify write permissions on uploads folder

---

## 📄 License

This project is licensed under the ISC License - see the `package.json` file for details.

---

## 👨‍💻 Author & Contact

**Your Name**
- GitHub: [Your GitHub Profile](https://github.com/yourusername)
- Email: your.email@example.com
- LinkedIn: [Your LinkedIn](https://linkedin.com/in/yourprofile)

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📞 Support

For issues, questions, or suggestions:
- Open an issue on GitHub
- Check existing issues and discussions
- Review documentation and troubleshooting section

---

**Last Updated**: April 2026  
**Project Status**: Active Development

---

## 🌟 If You Found This Helpful

Please consider giving this project a ⭐ star on GitHub!

