# 📘 Assignment: Test-Driven API Development with pytest

## 🎯 Objective

Extend your reading-list API using test-driven development: write a failing test, implement the smallest change that passes it, and refactor without breaking existing behavior. Use pytest and FastAPI's `TestClient` to verify filtering, validation, and error responses during this challenging, one-hour lab.

## 📝 Tasks

### 🛠️ Establish a Passing Test Baseline (8 minutes)

#### Description
Start with your working API from [Building REST APIs with FastAPI](../fastapi-rest-api/README.md), with `app` defined in `main.py`. Reuse its in-memory storage and CRUD endpoints rather than rebuilding the application.

In your activated project environment, install the test dependencies with `python -m pip install pytest httpx`. Create `tests/test_books.py`, import `app` from `main`, and use `TestClient` from `fastapi.testclient`. Run tests from the directory containing `main.py` with `python -m pytest -q`; a running development server is not needed.

#### Requirements
Completed program should:

- Provide a function-scoped pytest fixture that yields a `TestClient` inside a context manager.
- Start each test with an empty reading list and clean up afterward using the existing GET and DELETE endpoints; use fixture teardown with `yield` so cleanup also runs after an assertion fails.
- Pass a baseline test that asserts `GET /books` returns status `200` and `[]`.
- Create test data through `POST /books`, check that creation succeeds, and use returned IDs rather than assuming IDs start at `1`.

### 🛠️ Write Failing Tests for Read-Status Filtering (22 minutes)

#### Description
Define the new feature through tests before changing application code. Clients should be able to request only read or unread books using the optional `is_read` query parameter on `GET /books`.

For example, `GET /books?is_read=false` should return only unread books. Use `client.get("/books", params={"is_read": "false"})` to send the query parameter.

#### Requirements
Completed program should:

- Test that omitting `is_read` returns all books, including both read and unread books.
- Use `pytest.mark.parametrize` to test `"true"` and `"false"` against a dataset containing both statuses, asserting status `200` and exactly the expected book IDs and fields without depending on list order.
- Test that a valid filter with no matching books returns status `200` and `[]`.
- Test that `is_read=not-a-boolean` returns status `422` and a validation error identifying the `is_read` query parameter.
- Run the tests before implementing filtering and record at least one failing assertion caused by the missing feature, not by an import error or broken fixture.

### 🛠️ Implement the Feature and Protect Existing Behavior (20 minutes)

#### Description
Follow the red-green-refactor cycle: make the failing filter tests pass, then improve clarity while keeping the suite green. Use a typed optional boolean query parameter so FastAPI validates query input.

#### Requirements
Completed program should:

- Return all stored books when the filter is omitted, only read books for `true`, and only unread books for `false`; distinguish an omitted value from `False`.
- Return matching books without removing or modifying any stored books.
- Reject invalid boolean query values with status `422`.
- Pass a regression test that filters a mixed dataset and then confirms an unfiltered request still returns every original book unchanged.
- Use parameterized tests for POST bodies with a missing title, an empty title, or an empty author; assert status `422` and confirm each rejected request leaves stored data unchanged.
- Pass a test that creates and deletes a book, then retrieves its returned ID and asserts status `404` and `{"detail": "Book not found"}`.

### 🛠️ Prove Test Isolation and Explain the Cycle (10 minutes)

#### Description
Make sure your tests succeed because the API behaves correctly, not because another test left useful data behind. Keep assertions focused on observable API behavior rather than internal variable names.

#### Requirements
Completed program should:

- Pass the full suite with `python -m pytest -q`.
- Pass two data-creating tests individually and in both execution orders by supplying their pytest node IDs on the command line.
- Keep each test responsible for creating its own data, with no shared mutable test dataset or dependency on earlier tests.
- Continue to pass after refactoring repeated setup into fixtures or helpers, without weakening assertions.
- Be submitted with the updated application, test files, and a short submission note showing the initial feature-related failure, the final passing result, and how the fixture prevents state leakage.
