# Book Management API

A RESTful API for managing books with JWT authentication and role-based access control.

## Tech Stack

- Node.js
- Express.js
- MySQL
- Sequelize ORM
- JWT (JSON Web Tokens)
- Express Validator

## Prerequisites

- Node.js (v14 or higher)
- MySQL (v5.7 or higher)
- npm or yarn

## Installation

1. Clone the repository:
git clone https://github.com/Afsalbro/book-api.git
cd Book-Management


2. Install dependencies:
npm install


3. Create a `.env` file in the root directory:

PORT=3000
DB_HOST=localhost
DB_USER=root
DB_PASS=your_password
DB_NAME=book_management
JWT_SECRET=your_jwt_secret_key
JWT_EXPIRES_IN=24h


4. Create MySQL database:
CREATE DATABASE book_management;


5. Run the application:
# Development mode with nodemon
npm run dev

# Production mode
npm start


6. Run tests:
npm test


## Database Seeding

The application automatically seeds:
- An admin user
- 10 sample books

Default admin credentials:

Username: admin
Password: admin123


## API Endpoints

### Authentication

#### Register User
POST /auth/register
Content-Type: application/json

{
    "username": "testuser",
    "password": "password123",
    "role": "user"
}

Response:

{
    "message": "User registered successfully!"
}


#### Login
POST /auth/login
Content-Type: application/json

{
    "username": "admin",
    "password": "admin123"
}

Response:

{
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}


### Books

#### Get All Books (with pagination)
GET /books?page=1&limit=10

Response:

{
    "books": [
        {
            "id": 1,
            "title": "The Great Gatsby",
            "author": "F. Scott Fitzgerald",
            "genre": "Classic Fiction",
            "publishedYear": 1925
        },
        // ... more books
    ],
    "totalPages": 1,
    "currentPage": 1
}


#### Get Single Book
GET /books/1

Response:

{
    "id": 1,
    "title": "The Great Gatsby",
    "author": "F. Scott Fitzgerald",
    "genre": "Classic Fiction",
    "publishedYear": 1925
}


#### Create Book (Admin Only)
POST /books
Content-Type: application/json
x-access-token: <your-jwt-token>

{
    "title": "New Book",
    "author": "Author Name",
    "genre": "Fiction",
    "publishedYear": 2023
}

Response:

{
    "id": 11,
    "title": "New Book",
    "author": "Author Name",
    "genre": "Fiction",
    "publishedYear": 2023
}


#### Update Book (Admin Only)
PUT /books/1
Content-Type: application/json
x-access-token: <your-jwt-token>

{
    "genre": "Updated Genre"
}

Response:

{
    "id": 1,
    "title": "The Great Gatsby",
    "author": "F. Scott Fitzgerald",
    "genre": "Updated Genre",
    "publishedYear": 1925
}


#### Delete Book (Admin Only)
DELETE /books/1
x-access-token: <your-jwt-token>

Response:

{
    "message": "Book deleted successfully!"
}


## Error Responses

### Authentication Errors

{
    "message": "Unauthorized!"
}


### Validation Errors

{
    "errors": [
        {
            "msg": "Title is required",
            "param": "title",
            "location": "body"
        }
    ]
}


### Not Found

{
    "message": "Book not found!"
}


## Project Structure

src/
├── config/
│   └── db.config.js
├── controllers/
│   ├── auth.controller.js
│   └── book.controller.js
├── middleware/
│   └── auth.middleware.js
├── models/
│   ├── index.js
│   ├── user.model.js
│   └── book.model.js
├── routes/
│   ├── auth.routes.js
│   └── book.routes.js
├── seeders/
│   ├── adminSeeder.js
│   └── bookSeeder.js
├── __tests__/
│   ├── auth.test.js
│   └── book.test.js
└── index.js


## Testing

The project includes basic tests for authentication and book endpoints. Run tests using:
npm test


## Security Features

- Password hashing using bcrypt
- JWT-based authentication
- Role-based access control
- Input validation
- Environment variables for sensitive data
