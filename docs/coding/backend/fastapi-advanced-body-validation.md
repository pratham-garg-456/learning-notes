---
title: FastAPI Advanced Body Validation
---

# FastAPI Advanced Body Validation

## Body - Fields

```python
from typing import Annotated

from fastapi import Body, FastAPI
from pydantic import BaseModel, Field

app = FastAPI()

class Item(BaseModel):
    name: str
    description: str | None = Field(
        default=None, title="The description of the item", max_length=300
    )
    price: float = Field(gt=0, description="The price must be greater than zero")
    tax: float | None = None

@app.put("/items/{item_id}")
async def update_item(item_id: int, item: Annotated[Item, Body(embed=True)]):
    results = {"item_id": item_id, "item": item}
    return results
```

1. **Pydantic Model**:
    - `Item` defines the structure and validation rules for the request body:
        - `name`: Required string.
        - `description`: Optional string (max length: 300) with metadata (`title`).
        - `price`: Required float, must be greater than `0`.
        - `tax`: Optional float.
2. **Body with `embed=True`**:
    - Wrapping the entire request body inside an `"item"` key.
    - Expected request format:
        
        ```json
        //  PUT /items/1
        {
          "item": {
            "name": "New Item",
            "description": "A great item",
            "price": 10.99,
            "tax": 0.5
          }
        }
        ```
        
3. **Endpoint**:
    - Accepts `item_id` (path parameter) and `item` (embedded request body).
    - Returns both parameters in the response.

---

### **Response Example**

Valid Request:

```json
PUT /items/1
{
  "item": {
    "name": "New Item",
    "description": "A great item",
    "price": 10.99,
    "tax": 0.5
  }
}
```

Response:

JSON

```json
{
  "item_id": 1,
  "item": {
    "name": "New Item",
    "description": "A great item",
    "price": 10.99,
    "tax": 0.5
  }
}
```

Invalid Request:

```json
{
    "item_id": 1,
    "item": {
        "name": "New Item",
        "description": "A great item",
        "price": -10.99, //price is negative
        "tax": 0.5
    }
}
```

Response:

```json
{
    "detail": [
        {
            "loc": ["body", "item", "price"],
            "msg": "ensure this value is greater than 0",
            "type": "value_error.number.not_gt"
        }
    ]
}
```

---

###

## Practice Questions

??? question "1. How do you add validation rules to fields in a Pydantic body model?"

    Use `Field(...)`, for example `Field(gt=0, description=...)` for the price or `max_length=300` for the description.

??? question "2. What does Body(embed=True) do?"

    It expects the request body to be wrapped inside a key named after the parameter, for example `{ "item": { ... } }`.

??? question "3. What happens when a request breaks a rule, such as a negative price?"

    FastAPI returns a validation error with a detail list showing the location of the field (for example body, item, price) and the message.
