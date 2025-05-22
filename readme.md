
# Backend_assignment

A RESTful Task Management API built with Node.js, Express, and MongoDB featuring user and task management with JWT-based authentication.

## Table of Contents

- [Project Overview](#project-overview)  
- [Setup Instructions](#setup-instructions)  
- [Environment Variables](#environment-variables)  
- [API Documentation](#api-documentation)  
  - [User API Endpoints](#user-api-endpoints)  
  - [Task API Endpoints](#task-api-endpoints)
  - [API Response Format](#api-response-format)
  - [Standard Https Status Code used](#standard-https-status-code-used)
- [Git Version Control](#git-version-control)  
- [Bonus Features Implemented](#bonus-features-implemented)


## Project Overview

It is a simple yet robust backend API that allows you to manage users and tasks similar to basic features of Trello or Todoist. It supports JWT authentication for secure access.

## Setup Instructions

### Key Dependencies

This project uses the following main Node.js packages:

- **express** – Web framework
- **mongoose** – MongoDB ODM
- **jsonwebtoken** – JWT-based authentication
- **bcrypt** – Password hashing
- **dotenv** – Environment variable management
- **cookie-parser** – Cookie support
- **cors** – Enable cross-origin requests
- **nodemon** (dev) – Auto-restart server during development

To install all dependencies, simply run:
```
npm install package-name
```


### Installation

1. **Clone the repository**

```bash
git clone https://github.com/gauravai2025/Backend_assignment.git
cd Backend_assignment
```

2. **Install dependencies**

```bash
npm install
```

3. **Create `.env` file**

In the project root, create a `.env` file with:

```env
PORT=8000

# Replace <username>, <password>, <cluster-url>, and <database> as needed
MONGODB_URI=mongodb+srv://<username>:<password>@<cluster-url>/<database>?retryWrites=true&w=majority

JWT_SECRET=your_jwt_secret_key
ACCESS_TOKEN_EXPIRY=15m
REFRESH_TOKEN_EXPIRY=7d

```

4. **Run the server**

```bash
npm start
```

Server will run at `http://localhost:8000`

---

## Environment Variables

| Variable               | Description                      | Example                              |
|------------------------|----------------------------------|--------------------------------------|
| `PORT`                 | Port number to run the server    | 8000                                 |
| `MONGODB_URI`          | MongoDB connection string        | mongodb://user:pass@host:port/db     |
| `JWT_SECRET`           | Secret key for JWT token signing | your_secret_key_here                 |
| `ACCESS_TOKEN_EXPIRY`  | Access token expiration time     | 15m                                  |
| `REFRESH_TOKEN_EXPIRY` | Refresh token expiration time    | 7d                                   |

---

## API Documentation

### User API Endpoints

| Method | Endpoint               | Description                  | Request Body                                                                                     | Authentication |
|--------|------------------------|------------------------------|---------------------------------------------------------------------------------------------------|----------------|
| POST   | `/api/users/register`  | Register new user            | `{ "name": "gaurav kumar", "email": "gaurav170820@gmail.com", "password": "pass123" }`           | No             |
| POST   | `/api/users/login`     | Login user (get tokens)      | `{ "email": "gaurav170820@gmail.com", "password": "pass123" }`                                   | No             |
| POST   | `/api/users/logout`    | Logout user                  | Not required                                                                                      | No             |
| POST   | `/api/users/refresh`   | Refresh access token         | Not required (uses refresh token from cookies)                                                    | Yes (JWT)      |
| GET    | `/api/users/users/:id` | Get user details             | Not required                                                                                      | Yes (JWT)      |
| GET    | `/api/users/users`     | List all users               | Not required                                                                                      | Yes (JWT)      |
| GET    | `/api/users/me`        | Get current user profile     | Not required                                                                                      | Yes (JWT)      |


### Task API Endpoints


| Method | Endpoint            | Description                                                                                     | Request Body                                                                                                                      |
|--------|---------------------|-------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| POST   | `/api/tasks`        | Create new task                                                                                 | `{ "title": "Task 1", "description": "Details", "dueDate": "2025-06-01", "status": "pending", "assignedTo": "userId" }`          |
| GET    | `/api/tasks/:id`    | Get task details                                                                                | N/A                                                                                                                               |
| GET    | `/api/tasks`        | List tasks (e.g., `?status=pending&assignedTo=userId&page=1&limit=10`)                          | N/A                                                                                                                               |
| PUT    | `/api/tasks/:id`    | Update task                                                                                     | `{ "title": "Updated", "status": "completed" }`                                                                                   |
| DELETE | `/api/tasks/:id`    | Delete task                                                                                     | N/A                                                                                                                               |


---
## API Test Endpoints (Screenshots)
| Method | Endpoint              | Description              | Screenshot |
|--------|-----------------------|--------------------------|------------|
| POST   | `/api/users/register` | User registration        | <img src="screenshots/user_register.png" alt="User Registration" width="900"/> |
| POST   | `/api/users/login`    | User login (JWT)         | <img src="screenshots/user_login.png" alt="User Login" width="900"/> |
| GET    | `/api/users/me`       | Get current user profile | <img src="screenshots/access_currentUser.png" alt="Current User" width="900"/> |
| GET    | `/api/users/users/:id`| Get user details         | <img src="screenshots/user_details.png" alt="User Details" width="900"/> |
| POST   | `/api/users/refresh`  | Refresh access token     | <img src="screenshots/refresh_accessToken.png" alt="Refresh Token" width="900"/> |
| GET    | `/api/users/users`    | Get all users            | <img src="screenshots/getAllUsers.png" alt="All Users" width="900"/> |
| POST   | `/api/tasks`          | Create new task          | <img src="screenshots/addTask.png" alt="Add Task" width="900"/> |
| GET    | `/api/tasks/:id`      | Get task by ID           | <img src="screenshots/getTaskById.png" alt="Get Task" width="900"/> |
| GET    | `/api/tasks`          | Get all tasks            | <img src="screenshots/getAllTasks.png" alt="All Tasks" width="900"/> |
| PUT    | `/api/tasks/:id`      | Update task              | <img src="screenshots/updateTaskById.png" alt="Update Task" width="900"/> |
| DELETE | `/api/tasks/:id`      | Delete task              | <img src="screenshots/deleteTaskById.png" alt="Delete Task" width="900"/> |

## API Response Format

#### All API responses (success or error) follow a standard structure for consistency

### Success Response Format

```
 constructor(statusCode, data, message = "Success") {
        this.statusCode = statusCode;
        this.data = data;
        this.message = message;
        this.success = statusCode < 400;
    }
```
### Error Response Format

```
constructor(
        statusCode,
         message = "Something went wrong",
          errors = [], 
          stack = ""
        ) {
        super(message);
        this.statusCode = statusCode;
        this.data = null;
        this.message = message;
        this.success = false;
        this.errors = errors;

        if (stack) {
            this.stack = stack;
        }
         else {
            Error.captureStackTrace(this, this.constructor);
        }
    }

```
## Standard Https Status Code used
| Code | Scenario                                                                 |
|------|--------------------------------------------------------------------------|
| 200  | OK – The request was successful and the server returned the expected response |
| 201  | Created – The request was successful and a new resource was created      |
| 400  | Bad Request – Invalid request body or missing required fields            |
| 401  | Unauthorized – Missing or invalid JWT token                              |
| 403  | Forbidden – User does not have permission to access the resource         |
| 404  | Not Found – The requested resource was not found                         |
| 500  | Internal Server Error – A generic server-side error occurred             |



## Git Version Control

```bash
# Commit example
git commit -m "feat: add JWT authentication middleware"
git commit -m "fix: correct task status validation"
```

Repository: [Backend Assignment](https://github.com/gauravai2025/Backend_assignment)
=======
* The project uses Git for version control.
* Commits follow meaningful, clear messages.

---

## Bonus Features Implemented

✅ JWT Authentication with access/refresh tokens  
✅ Comprehensive error handling  
✅ API documentation with examples  
✅ Pagination and filtering  
✅ Environment configuration  
✅ Automated testing (Postman/thunder client)  


