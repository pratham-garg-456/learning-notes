---
title: FastAPI Advanced Route Validation
---

# FastAPI Advanced Route Validation

## **Annotated Parameters in FastAPI**

FastAPI uses Python 3.9's `Annotated` feature to add metadata and validation to parameters, useful for **query parameters**, **path parameters**, and **headers**.

---

### **How Annotated Works**

Use `Annotated` from `typing` module with FastAPI's validation classes to add metadata to type hints.

#### **Syntax:**

```python
from typing import Annotated
```

#### **Example:**

```python
from typing import Annotated
from fastapi import FastAPI, Query

app = FastAPI()

@app.get("/items/")
def read_items(limit: Annotated[int, Query(gt=0, le=100, description="Limit must be >=0 and <=100")]):
    return {"limit": limit}
```

Here, `limit` is:

- Annotated with a type (`int`).
- Given metadata using FastAPI's `Query` class (`gt=0` means greater than 0, `le=100` means less than or equal to 100).

---

### **Parameter Types**

Annotated works with three main parameter types:

- Query Parameters: Add validation rules and descriptions
- Path Parameters: Use with `Path` class for route validation
- Headers: Use with `Header` class for request headers

---

### **Benefits**

1. **Clearer Code**: Combines type hints with validation
2. **Extra Metadata**: Adds constraints without affecting types
3. **Better Documentation**: Improves API documentation
4. **Flexibility**: Works with all FastAPI validation classes

### **Query Parameters with a Pydantic Model**

```python
from typing import Annotated, Literal

from fastapi import FastAPI, Query
from pydantic import BaseModel, Field

app = FastAPI()

class QueryParams(BaseModel):
    limit: int = Field(100, gt=0, le=100)
    offset: int = Field(0, ge=0)
    order_by: Literal["created_at", "updated_at"] = "created_at"
    tags: list[str] = []

@app.get("/items/")
async def read_items(filter_query: Annotated[QueryParams, Query()]):
    return filter_query
```

**Invalid Request Example:**

```json
/items/?limit=200&offset=-1
```

**Response:**

```json
{
    "detail": [
        {
            "loc": ["query", "limit"],
            "msg": "ensure this value is less than or equal to 100",
            "type": "value_error.number.not_le"
        },
        {
            "loc": ["query", "offset"],
            "msg": "ensure this value is greater than or equal to 0",
            "type": "value_error.number.not_ge"
        }
    ]
}
```

## Practice Questions

??? question "1. What does Annotated add to a FastAPI parameter?"

    It attaches metadata and validation (from classes like `Query`, `Path`, and `Header`) to a type hint, without changing the type itself.

??? question "2. What do gt=0 and le=100 mean in Query(gt=0, le=100)?"

    The value must be greater than 0 and less than or equal to 100.

??? question "3. What are the benefits of Annotated?"

    Clearer code (type hints and validation together), extra metadata without affecting types, better API documentation, and flexibility across all FastAPI validation classes.

??? question "4. How can you validate a group of query parameters together?"

    Define a Pydantic model with `Field` constraints and use `Annotated[QueryParams, Query()]`. An invalid request returns a detail list naming each failed parameter.
