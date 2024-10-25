### Rule Engine Project

This project is a custom rule-based engine allowing users to create, store, and evaluate logical rules against specific data sets. It incorporates:

- A **Flask** backend to manage rule creation and evaluation operations
- **MongoDB** for rule persistence and storage
- A **React** frontend that provides an interactive user interface

---

### Key Features

- **Rule Creation**: Users can define rules using conditional expressions, like `age > 30 AND salary > 50000`.
- **Rule Evaluation**: Users can test created rules against custom data entries.
- **Data Storage**: Rules are stored in **MongoDB** to ensure persistence and easy access.
- **Client-Server Communication**: Frontend communicates with the backend via HTTP requests to create and evaluate rules.
- **Error Handling**: Comprehensive error handling on both frontend and backend ensures stability.

---

### Table of Contents

- [Technologies](#technologies)
- [Setup Guide](#setup-guide)
- [Backend Configuration](#backend-configuration)
- [Frontend Configuration](#frontend-configuration)
- [Usage Instructions](#usage-instructions)
- [API Documentation](#api-documentation)
- [License](#license)

---

### Technologies

- **Backend**: Flask, Flask-CORS, pymongo
- **Database**: MongoDB
- **Frontend**: React, Axios
- **Additional**: Python’s `ast` module for parsing rule expressions into an Abstract Syntax Tree (AST)

---

### Setup Guide

#### Prerequisites

- **Node.js**: Required for running the React frontend
- **Python 3.x**: Required for running the Flask backend
- **MongoDB**: Either locally or remotely accessible

#### Installation Steps

- Clone the repository locally:
  ```bash
  git clone https://github.com/yourusername/rule-engine-project.git
  cd rule-engine-project
  ```

---

### Backend Configuration

1. Change directory to `backend/`:
   ```bash
   cd backend/
   ```
2. Install the required Python dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Confirm MongoDB is running locally or update the `MongoClient` connection in `app.py` to point to a remote MongoDB instance:
   ```python
   client = MongoClient('mongodb://localhost:27017/')
   ```
4. Start the Flask server:
   ```bash
   python app.py
   ```
   - The backend will run at `http://localhost:5000`.

---

### Frontend Configuration

1. Change to the `frontend/` directory:
   ```bash
   cd frontend/
   ```
2. Install the necessary packages:
   ```bash
   npm install
   ```
3. Start the React server:
   ```bash
   npm start
   ```
   - The frontend will be accessible at `http://localhost:3000`.

---

### Usage Instructions

1. **Creating a Rule**
   - Access the "Create Rule" section from the homepage.
   - Define a rule using a logical string, such as `age > 30 AND salary > 50000`.
   - Submit the rule by clicking "Create Rule". A confirmation message with a unique rule ID will be provided.

2. **Evaluating a Rule**
   - Open the "Evaluate Rule" section on the homepage.
   - Input the rule ID and the data (in JSON format) to check against the rule. Example data:
     ```json
     { "age": 35, "salary": 60000 }
     ```
   - Click "Evaluate Rule" to view the evaluation result (either true or false).

---

### API Documentation

#### 1. Create Rule Endpoint
- **URL**: `/api/create_rule`
- **Method**: POST
- **Request Body**:
  ```json
  { "rule": "age > 30 AND salary > 50000" }
  ```
- **Response**:
  - **Success** (201 Created):
    ```json
    { "message": "Rule created successfully", "rule_id": "6144f0e1f3b60f2f5b6a254e" }
    ```
  - **Error** (400 Bad Request):
    ```json
    { "error": "Rule string is required" }
    ```

#### 2. Evaluate Rule Endpoint
- **URL**: `/api/evaluate_rule`
- **Method**: POST
- **Request Body**:
  ```json
  {
    "rule_id": "6144f0e1f3b60f2f5b6a254e",
    "data": { "age": 35, "salary": 60000 }
  }
  ```
- **Response**:
  - **Success** (200 OK):
    ```json
    { "result": true }
    ```
  - **Error** (404 Not Found):
    ```json
    { "error": "Rule not found" }
    ```
