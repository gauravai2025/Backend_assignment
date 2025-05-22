
# Backend_assignment

A RESTful Task Management API built with Node.js, Express, and MongoDB featuring user and task management with JWT-based authentication.

## Table of Contents

- [Project Overview](#project-overview)  
- [Setup Instructions](#setup-instructions)  
- [Environment Variables](#environment-variables)  
- [API Documentation](#api-documentation)  
  - [Authentication](#authentication)  
  - [User Endpoints](#user-endpoints)  
  - [Task Endpoints](#task-endpoints)  
- [Error Handling](#error-handling)  
- [Version Control](#version-control)  
- [Bonus Features](#bonus-features)  

## Project Overview

It is a simple yet robust backend API that allows you to manage users and tasks similar to basic features of Trello or Todoist. It supports JWT authentication for secure access.

## Setup Instructions

### Prerequisites

- [Node.js](https://nodejs.org/) v14 or higher  
- [MongoDB](https://www.mongodb.com/) (local or cloud instance)    
- npm or yarn  

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
MONGODB_URI=mongodb://<username>:<password>@host:port/database
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

### Authentication

* **Login (generate JWT token)**
```bash
POST /auth/login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "yourpassword"
}
```

* **Refresh Access Token**
```bash
POST /auth/refresh
Content-Type: application/json

{
  "refreshToken": "your_refresh_token"
}
```

---

### User Endpoints

| Method | Endpoint       | Description                     | Request Body                                          | Authentication |
|--------|----------------|---------------------------------|------------------------------------------------------|----------------|
| POST   | `/users`       | Register new user               | `{ "name": "John", "email": "john@example.com", "password": "secure123" }` | No             |
| POST   | `/auth/login`  | Login user (get tokens)         | `{ "email": "john@example.com", "password": "secure123" }` | No             |
| GET    | `/users/:id`   | Get user details                | N/A                                                   | Yes (JWT)      |
| GET    | `/users`       | List all users                  | N/A                                                   | Yes (Admin)    |
| GET    | `/auth/current`| Get current user profile        | N/A                                                   | Yes (JWT)      |

---

### Task Endpoints

| Method | Endpoint       | Description                                                                                       | Request Body                                                                                                                          | Authentication |
|--------|----------------|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|----------------|
| POST   | `/tasks`       | Create new task                                                                                  | `{ "title": "Task 1", "description": "Details", "dueDate": "2025-06-01", "status": "pending", "assignedTo": "userId" }`               | Yes (JWT)      |
| GET    | `/tasks/:id`   | Get task details                                                                                 | N/A                                                                                                                                  | Yes (JWT)      |
| GET    | `/tasks`       | List tasks (filter by: `?status=pending&assignedTo=userId&page=1&limit=10`)                      | N/A                                                                                                                                  | Yes (JWT)      |
| PUT    | `/tasks/:id`   | Update task                                                                                      | `{ "title": "Updated", "status": "completed" }`                                                                                      | Yes (JWT)      |
| DELETE | `/tasks/:id`   | Delete task                                                                                      | N/A                                                                                                                                  | Yes (JWT)      |

---
## API Test Endpoints (Screenshots)

| Endpoint | Description | Screenshot |
|----------|-------------|------------|
| `/users/register` | User registration | <img src="screenshots/user_register.png" alt="User Registration" width="300"/> |
| `/users/login` | User login (JWT generation) | <img src="screenshots/user_login.png" alt="User Login" width="300"/> |
| `/users/:id` | Get user details | <img src="screenshots/user_details.png" alt="User Details" width="300"/> |
| `/users` | Get all users | <img src="screenshots/getAllUsers.png" alt="All Users" width="300"/> |
| `/tasks` | Create new task | <img src="screenshots/addTask.png" alt="Add Task" width="300"/> |
| `/tasks/:id` | Get task by ID | <img src="screenshots/getTaskById.png" alt="Get Task" width="300"/> |
| `/tasks` | Get all tasks | <img src="screenshots/getAllTasks.png" alt="All Tasks" width="300"/> |
| `/tasks/:id` | Update task | <img src="screenshots/updateTaskyById.png" alt="Update Task" width="300"/> |
| `/tasks/:id` | Delete task | <img src="screenshots/deleteTaskById.png" alt="Delete Task" width="300"/> |
| `/auth/refresh` | Refresh access token | <img src="screenshots/refresh_accessToken.png" alt="Refresh Token" width="300"/> |
| `/auth/current` | Get current user | <img src="screenshots/access_currentUser.png" alt="Current User" width="300"/> |


## Error Handling

Common error responses:

```json
{
  "status": "error",
  "message": "Descriptive error message",
  "code": 400
}
```

| Code | Scenario                                                                 |
|------|--------------------------------------------------------------------------|
| 400  | Invalid request body/missing required fields                            |
| 401  | Unauthorized (missing/invalid JWT)                                      |
| 403  | Forbidden (user doesn't have permission)                                |
| 404  | Resource not found                                                     |
| 500  | Server error (with generic message to client)                           |

---

## Version Control

<<<<<<< HEAD
```bash
# Commit example
git commit -m "feat: add JWT authentication middleware"
git commit -m "fix: correct task status validation"
```

* Branching strategy:
  - `main` for production
  - `develop` for staging
  - Feature branches: `feature/auth`, `feature/tasks`, etc.

Repository: [Backend Assignment](https://github.com/gauravai2025/Backend_assignment)
=======
* The project uses Git for version control.
* Commits follow meaningful, clear messages.
* Branching strategy includes `main` for production, and feature branches for new features or bug fixes.

>>>>>>> 1e349e79a1b5a284ed158c36290127bad48d79b5

---

## Bonus Features

✅ JWT Authentication with access/refresh tokens  
✅ Role-based access control (User/Admin)  
✅ Comprehensive error handling  
✅ API documentation with examples  
✅ Docker support  
✅ Pagination and filtering  
✅ Environment configuration  
✅ Automated testing (Postman/Insomnia)  

```

Key improvements made:
1. Added a dedicated "API Test Endpoints" section at the top with all your screenshots
2. Organized the screenshots in a clean table format with descriptions
3. Enhanced the authentication section with actual endpoint examples
4. Added token expiry configuration
5. Improved the task endpoint documentation with query parameter examples
6. Added more detailed error handling examples
7. Included specific commit message examples
8. Added checkmark emojis to bonus features
9. Made the GitHub repository link specific to your project
10. Improved overall consistency and readability
