---
title: FastAPI Routes
---

# FastAPI Routes

In FastAPI, routes define the endpoints where a client can send HTTP requests. Each route is associated with a specific path and HTTP method (GET, POST, PUT, DELETE, etc.).

## Example of routes

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/items")
def get_items():
    return {"message": "List of items"}

@app.post("/items")
def create_item(item: dict):
    return {"message": "Item created", "item": item}
```

## Route parameters

Route parameters define dynamic parts of the URL. They are specified in the path using curly braces `{}`.

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/items/{item_id}")
def get_item(item_id: int):
    return {"item_id": item_id}
```

- `{item_id}` is a route parameter.
- The route `/items/42` matches and returns `{"item_id": 42}`.

!!! tip "Specific routes before generic routes"
    If you have routes with overlapping paths, make sure the more specific route is defined first.

    ```python
    @app.get("/items/{item_id}")
    def get_item_by_id(item_id: int):
        return {"item_id": item_id}

    @app.get("/items/special")
    def get_special_items():
        return {"message": "Special items"}
    ```

    Here the `/items/special` route is never reached, because `/items/{item_id}` matches `/items/special` first. To fix this, place the `/items/special` route before `/items/{item_id}`.

## Query parameters

Query parameters are appended to the URL after a `?` and pass key-value pairs. They are commonly used for optional parameters.

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/search")
def search_items(q: str = None, limit: int = 10):
    return {"query": q, "limit": limit}
```

- `q` and `limit` are query parameters.
- The route `/search?q=books&limit=5` returns `{"query": "books", "limit": 5}`.

## Combining route parameters and query parameters

You can use both together to create more complex endpoints.

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/users/{user_id}/items")
def get_user_items(user_id: int, item_type: str = None, limit: int = 10):
    return {"user_id": user_id, "item_type": item_type, "limit": limit}
```

- `{user_id}` is a route parameter.
- `item_type` and `limit` are query parameters.
- The route `/users/123/items?item_type=book&limit=5` returns:

```json
{"user_id": 123, "item_type": "book", "limit": 5}
```

## Optional and default together

You can combine optional parameters with default values.

```python
from typing import Optional
from fastapi import FastAPI

app = FastAPI()

@app.get("/items/")
def read_item(name: Optional[str] = "Guest"):
    return {"message": f"Hello, {name}!"}
```

- `name` is an optional query parameter with a default value of `"Guest"`.
- `/items/?name=John` returns `{"message": "Hello, John!"}`.
- `/items/` without `name` returns `{"message": "Hello, Guest!"}`.

## POST method

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

# Define a Pydantic model for request data validation
class Item(BaseModel):
    name: str
    description: str
    price: float
    in_stock: bool

@app.post("/items/")
def create_item(item: Item):
    return {
        "message": "Item created successfully!",
        "item": item
    }
```

1. **Pydantic model.** The `Item` class is defined using Pydantic's `BaseModel`. It ensures the request payload matches the expected structure and types.
2. **Request body.** When a client sends a POST request to `/items/` with JSON like:

    ```json
    {
        "name": "Laptop",
        "description": "A powerful gaming laptop",
        "price": 1500.00,
        "in_stock": true
    }
    ```

    FastAPI parses the JSON, validates it against the `Item` model, and passes it to the function.
3. **Response.** The server returns the JSON response:

    ```json
    {
        "message": "Item created successfully!",
        "item": {
            "name": "Laptop",
            "description": "A powerful gaming laptop",
            "price": 1500.0,
            "in_stock": true
        }
    }
    ```

## Practice Questions

??? question "1. What is a route in FastAPI?"

    An endpoint where a client can send HTTP requests. Each route is tied to a specific path and HTTP method (GET, POST, PUT, DELETE, and so on).

??? question "2. What is the difference between a route parameter and a query parameter?"

    A route parameter is a dynamic part of the path, written in curly braces (`/items/{item_id}`). A query parameter is a key-value pair after `?` in the URL (`/search?q=books&limit=5`), commonly used for optional values.

??? question "3. Why would /items/special never be reached if it is defined after /items/{item_id}?"

    Routes are matched in order, and `/items/{item_id}` matches `/items/special` first. Define the more specific route before the generic one.

??? question "4. What does a Pydantic model do in a POST route?"

    It defines the expected structure and types of the request body. FastAPI parses the incoming JSON, validates it against the model, and passes it to the function.

??? question "5. What does /items/ return with no name, given name: Optional[str] = Guest?"

    `{"message": "Hello, Guest!"}`, because the optional query parameter falls back to its default value.
