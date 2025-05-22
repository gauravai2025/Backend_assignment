
````markdown
# Taskify

A RESTful Task Management API built with Node.js, Express, and MongoDB featuring user and task management with JWT-based authentication.

---

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

---

## Project Overview

Taskify is a simple yet robust backend API that allows you to manage users and tasks similar to basic features of Trello or Todoist. It supports JWT authentication for secure access.

## Setup Instructions

### Prerequisites

- [Node.js](https://nodejs.org/) v14 or higher  
- [MongoDB](https://www.mongodb.com/) (local or cloud instance)    
- npm or yarn  

### Installation

1. **Clone the repository**

```bash
git clone https://github.com/your-username/Backend_assignment.git
cd Backend_assignment
````

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
```

4. **Run the server**

```bash
npm start
```

Server will run at `http://localhost:8000`

---

## Environment Variables

| Variable      | Description                      | Example                              |
| ------------- | -------------------------------- | ------------------------------------ |
| `PORT`        | Port number to run the server    | 8000                                 |
| `MONGODB_URI` | MongoDB connection string        | mongodb://<username>:<password>@host:port/database |
| `JWT_SECRET`  | Secret key for JWT token signing | your\_secret\_key\_here              |

---

## API Documentation

### Authentication

* **Login (generate JWT token)**

> For this assignment, you may have a simple token issuance or use user creation for token generation. (Adjust if applicable)

---

### User Endpoints

| Method | Endpoint     | Description       | Request Body                                          | Authentication |
| ------ | ------------ | ----------------- | ----------------------------------------------------- | -------------- |
| POST   | `/users`     | Create a new user | `{ "name": "John Doe", "email": "john@example.com" }` | No             |
| GET    | `/users/:id` | Get user details  | N/A                                                   | Yes            |
| GET    | `/users`     | List all users    | N/A                                                   | Yes            |

---

### Task Endpoints

| Method | Endpoint     | Description                                                                                       | Request Body                                                                                                                          | Authentication |
| ------ | ------------ | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- | -------------- |
| POST   | `/tasks`     | Create a new task                                                                                 | `{ "title": "Task 1", "description": "Details", "dueDate": "2025-06-01T12:00:00Z", "status": "pending", "assignedUserId": "userId" }` | Yes            |
| GET    | `/tasks/:id` | Get task details                                                                                  | N/A                                                                                                                                   | Yes            |
| GET    | `/tasks`     | List tasks (with optional filters: `status`, `assignedUserId`, pagination params `page`, `limit`) | N/A                                                                                                                                   | Yes            |
| PUT    | `/tasks/:id` | Update task details                                                                               | `{ "title": "Updated title", "status": "completed" }`                                                                                 | Yes            |
| DELETE | `/tasks/:id` | Delete a task                                                                                     | N/A                                                                                                                                   | Yes            |

---

### Sample Requests and Responses

**Create User**

```bash
POST /users
Content-Type: application/json

{
  "name": "Alice",
  "email": "alice@example.com"
}
```

**Response**

```json
{
  "status": "success",
  "data": {
    "user": {
      "_id": "60d0fe4f5311236168a109ca",
      "name": "Alice",
      "email": "alice@example.com"
    }
  }
}
```

---

**Create Task**

```bash
POST /tasks
Authorization: Bearer <token>
Content-Type: application/json

{
  "title": "Finish README",
  "description": "Write the README file for the project",
  "dueDate": "2025-06-01T12:00:00Z",
  "status": "pending",
  "assignedUserId": "60d0fe4f5311236168a109ca"
}
```

**Response**

```json
{
  "status": "success",
  "data": {
    "task": {
      "_id": "60d0fe9f5311236168a109cb",
      "title": "Finish README",
      "description": "Write the README file for the project",
      "dueDate": "2025-06-01T12:00:00Z",
      "status": "pending",
      "assignedUserId": "60d0fe4f5311236168a109ca",
      "createdAt": "2025-05-22T08:30:00Z"
    }
  }
}
```

---

## Error Handling

* Returns appropriate HTTP status codes (400, 401, 404, 500)
* Validates required fields and returns descriptive error messages
* Returns `401 Unauthorized` if JWT token is missing or invalid
* Returns `404 Not Found` if requested user/task does not exist
* Handles unexpected server errors gracefully with a generic message

---

## Version Control

* The project uses Git for version control.
* Commits follow meaningful, clear messages.
* Branching strategy includes `main` for production, and feature branches for new features or bug fixes.
* GitHub (or GitLab/Bitbucket) repo link: [https://github.com/your-username/taskify](https://github.com/your-username/taskify)

---

## Bonus Features

* JWT-based authentication for securing API endpoints
* Pagination support on task listing endpoints (`page` and `limit` query params)
* Environment variable configuration using `.env` file
* Dockerfile for containerizing the application

