# 📘 Assignment: Building REST APIs with FastAPI

## 🎯 Objective

Build a REST API for managing a reading list using FastAPI. Practice HTTP methods, JSON request and response bodies, data validation, and status codes while creating and testing endpoints.

## 📝 Tasks

### 🛠️ Create and Run Your First Endpoint

#### Description
Start with a small success: create a FastAPI application that responds to a request. You should already be comfortable with Python functions, dictionaries, and classes.

Create a project folder and a virtual environment using `python -m venv .venv`. Activate it with `source .venv/bin/activate` on macOS/Linux or `.venv\Scripts\Activate.ps1` in Windows PowerShell, then install FastAPI with `python -m pip install "fastapi[standard]"`.

#### Requirements
Completed program should:

- Define a FastAPI application named `app` in a file named `main.py`.
- Provide a `GET /` endpoint that returns `{"message": "Welcome to the Reading List API"}` with status `200 OK`.
- Run locally using `fastapi dev main.py`.
- Display interactive API documentation at `http://127.0.0.1:8000/docs`; use its **Try it out** button to check the welcome endpoint.

### 🛠️ Retrieve Books from the Reading List

#### Description
Use an in-memory list or dictionary to store books and add endpoints for reading them. Each book should have an integer `id`, a string `title`, a string `author`, and a boolean `is_read`.

Keep this assignment focused on API design: no database, authentication, or deployment is required. Stored books reset when the server restarts or reloads.

#### Requirements
Completed program should:

- Provide `GET /books` to return all stored books as a JSON array with status `200 OK`; return `[]` when the list is empty.
- Provide `GET /books/{book_id}` to return the matching book with status `200 OK`.
- Treat `book_id` as an integer path parameter.
- Raise FastAPI's `HTTPException` with status `404 Not Found` and detail `"Book not found"` when an integer ID does not exist.

Example response for a stored book:

```json
{
  "id": 1,
  "title": "The Python Explorer",
  "author": "Alex Rivera",
  "is_read": false
}
```

### 🛠️ Add Books with Validated Request Bodies

#### Description
Use a Pydantic model to describe the JSON body for creating a book. Let the server assign IDs rather than asking the client to choose them.

#### Requirements
Completed program should:

- Define a request model with required, non-empty string fields `title` and `author`, and a boolean `is_read` that defaults to `False`.
- Provide `POST /books` to validate the request body, store the new book, and return it with status `201 Created`.
- Assign each new book a unique integer ID that is not reused after deletion during the same server run.
- Leave stored data unchanged and return FastAPI's validation response with status `422 Unprocessable Entity` when required fields are missing or a title or author is an empty string.
- Make newly created books available through both GET endpoints.

Example request body:

```json
{
  "title": "The Python Explorer",
  "author": "Alex Rivera"
}
```

### 🛠️ Update, Delete, and Test Books

#### Description
Complete the create, read, update, and delete (CRUD) workflow. Use the interactive documentation to check successful requests and error cases.

#### Requirements
Completed program should:

- Provide `PUT /books/{book_id}` to replace a book's editable fields using a validated request model where `title`, `author`, and `is_read` are all required.
- Preserve the book's ID and return the updated book with status `200 OK`; reject empty titles or authors with status `422` without changing the stored book.
- Provide `DELETE /books/{book_id}` to remove an existing book and return status `204 No Content` with an empty response body.
- Return status `404` and detail `"Book not found"` when an integer ID does not exist for an update or deletion.
- Demonstrate this sequence in `/docs`: create a book, list books, retrieve it by ID, mark it as read using PUT, delete it, and confirm that retrieving it now returns `404`.
- Check that creating a book without a title returns `422`, updating a book without `is_read` returns `422`, and requesting `/books/not-a-number` returns `422`.
