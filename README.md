Sure! Let's learn **APIs in React.js** in a very simple way. One important thing to know first is:

> **React itself does not have APIs like GET, POST, PUT, DELETE, or PATCH.**
> These are **HTTP methods** used to communicate with a **backend server** or **database**. React simply sends requests to the API and displays the response.

---

# What is an API?

**API** stands for **Application Programming Interface**.

Think of an API like a **waiter in a restaurant**.

* 👨 You = React application
* 🍽️ Waiter = API
* 👨‍🍳 Kitchen = Server/Database

Example:

1. You order a pizza.
2. The waiter takes your order to the kitchen.
3. The kitchen prepares the pizza.
4. The waiter brings the pizza back.

Similarly:

1. React sends a request.
2. API receives it.
3. Server processes it.
4. API sends data back.

```
React App
     |
     | Request
     ↓
    API
     |
     ↓
 Server / Database
     |
     ↑
 Response
     |
React App
```

---

# Real Example

Imagine a **Student Management System**.

Database:

| ID | Name  | Age |
| -- | ----- | --- |
| 1  | John  | 22  |
| 2  | Emma  | 20  |
| 3  | David | 21  |

React communicates with the server using APIs.

---

# HTTP Methods

There are five main methods you'll use most often:

| Method | Purpose                 |
| ------ | ----------------------- |
| GET    | Read data               |
| POST   | Add new data            |
| PUT    | Update all data         |
| PATCH  | Update part of the data |
| DELETE | Remove data             |

Let's understand each one.

---

# 1. GET

GET means:

> "Please send me the data."

Example:

```
GET /students
```

Server returns:

```json
[
  {
    "id":1,
    "name":"John",
    "age":22
  },
  {
    "id":2,
    "name":"Emma",
    "age":20
  }
]
```

React displays:

```
John
Emma
```

---

### React Example

```jsx
import { useEffect, useState } from "react";

function App() {
  const [students, setStudents] = useState([]);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((response) => response.json())
      .then((data) => setStudents(data));
  }, []);

  return (
    <div>
      {students.map((student) => (
        <p key={student.id}>{student.name}</p>
      ))}
    </div>
  );
}

export default App;
```

### Flow

```
React
   ↓
GET request
   ↓
API
   ↓
Database
   ↓
Data
   ↓
React Screen
```

---

# 2. GET by ID

Sometimes you only want one record.

Example:

```
GET /students/2
```

Server returns:

```json
{
    "id":2,
    "name":"Emma",
    "age":20
}
```

Instead of all students, you get only Emma.

React:

```javascript
fetch("https://jsonplaceholder.typicode.com/users/2")
```

---

# 3. POST

POST means:

> "Add new data."

Suppose a user fills out this form:

```
Name : Alice
Age : 23
```

React sends:

```json
{
    "name":"Alice",
    "age":23
}
```

API saves it.

Database becomes:

| ID | Name  | Age |
| -- | ----- | --- |
| 1  | John  | 22  |
| 2  | Emma  | 20  |
| 3  | Alice | 23  |

---

### React Example

```jsx
fetch("https://jsonplaceholder.typicode.com/users", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    name: "Alice",
    age: 23,
  }),
});
```

---

# 4. PUT

PUT means:

> Replace the **entire record**.

Current record:

```json
{
    "id":1,
    "name":"John",
    "age":22
}
```

You send:

```json
{
    "name":"Peter",
    "age":30
}
```

Result:

```json
{
    "id":1,
    "name":"Peter",
    "age":30
}
```

Everything is replaced with the new values.

---

### React Example

```jsx
fetch("https://jsonplaceholder.typicode.com/users/1", {
  method: "PUT",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    name: "Peter",
    age: 30,
  }),
});
```

---

# 5. PATCH

PATCH means:

> Update only the fields you specify.

Current data:

```json
{
    "id":1,
    "name":"John",
    "age":22
}
```

You send:

```json
{
    "age":25
}
```

Result:

```json
{
    "id":1,
    "name":"John",
    "age":25
}
```

Only the age changes. The name stays the same.

---

### React Example

```jsx
fetch("https://jsonplaceholder.typicode.com/users/1", {
  method: "PATCH",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    age: 25,
  }),
});
```

---

# 6. DELETE

DELETE means:

> Remove the data.

Current table:

| ID | Name  |
| -- | ----- |
| 1  | John  |
| 2  | Emma  |
| 3  | David |

Request:

```
DELETE /students/2
```

Result:

| ID | Name  |
| -- | ----- |
| 1  | John  |
| 3  | David |

Emma's record is removed.

---

### React Example

```jsx
fetch("https://jsonplaceholder.typicode.com/users/2", {
  method: "DELETE",
});
```

---

# Summary Table

| Method    | What it does             | Example                          |
| --------- | ------------------------ | -------------------------------- |
| GET       | Read all data            | Get all students                 |
| GET by ID | Read one record          | Get student with ID 2            |
| POST      | Add new data             | Add a new student                |
| PUT       | Replace an entire record | Replace all details of a student |
| PATCH     | Update part of a record  | Change only the student's age    |
| DELETE    | Remove a record          | Delete a student                 |

---

# Everyday Analogy

Imagine a notebook where you keep your contacts.

* **GET** 📖 → Read all contacts.
* **GET by ID** 🔍 → Find one contact by its number.
* **POST** ➕ → Add a new contact.
* **PUT** ✏️ → Rewrite all the details for a contact.
* **PATCH** 📝 → Correct just one detail, like the phone number.
* **DELETE** 🗑️ → Erase a contact.

---

# Typical React API Flow

```
User clicks a button
        │
        ▼
React sends an HTTP request (GET/POST/PUT/PATCH/DELETE)
        │
        ▼
Backend API receives the request
        │
        ▼
Database is read or updated
        │
        ▼
Backend sends a response (usually JSON)
        │
        ▼
React updates the UI
```

---

# Practice API

A good free API for learning is **JSONPlaceholder**:

```
GET    https://jsonplaceholder.typicode.com/posts
GET    https://jsonplaceholder.typicode.com/posts/1
POST   https://jsonplaceholder.typicode.com/posts
PUT    https://jsonplaceholder.typicode.com/posts/1
PATCH  https://jsonplaceholder.typicode.com/posts/1
DELETE https://jsonplaceholder.typicode.com/posts/1
```

> **Note:** JSONPlaceholder is a fake API for practice. It accepts requests and returns sample responses, but it doesn't permanently save changes.

As you continue learning React, you'll often use these methods together with `fetch()` or libraries like Axios to communicate with backend APIs.
