---
title: Beanie
---

# Beanie

## What is Beanie?

- An asynchronous Python Object-Document Mapper (ODM).
- The data models of Beanie are based on Pydantic (a tool for data validation).

!!! tip
    You can use a MongoDB Docker image instead of a real MongoDB to connect with MongoDB too ([YouTube walkthrough](https://youtu.be/ZrJnc8j6jkg?si=egoAx5RJ79iT8uqr)).

## 1. Model folder

**Purpose.** Contains classes that define how your data is stored or mapped in the database.

**What's inside**

- ORM/ODM models (for example SQLAlchemy models for relational databases, ODMantic or Beanie models for MongoDB).
- Each model class typically represents a table (RDBMS) or a collection (NoSQL) in your database.
- Fields, types, and sometimes methods for database interaction.

**Example**

```python
# models/user.py
from beanie import Document

class User(Document):
    name: str
    email: str
```

## 2. Schema folder

**Purpose.** Contains Pydantic classes for data validation, serialization, and deserialization (input and output).

**What's inside**

- Pydantic models used to validate request and response data (for example for API endpoints).
- Classes can exclude sensitive or internal fields, or include extra fields for output only.
- Keeps a clear separation between how data is stored (model) and how it is exposed or received (schema).

**Example**

```python
# schemas/user.py
from pydantic import BaseModel, EmailStr

class UserCreate(BaseModel):
    name: str
    email: EmailStr

class UserRead(BaseModel):
    id: str
    name: str
    email: EmailStr
```

## Summary

| Folder | Purpose | Used for | Typical content |
| --- | --- | --- | --- |
| models | Database mapping | DB storage and queries | ORM/ODM classes |
| schemas | Data validation | API input/output, serialization | Pydantic models |

## Practice Questions

??? question "1. What is Beanie?"

    An asynchronous Python Object-Document Mapper (ODM) for MongoDB, whose data models are based on Pydantic.

??? question "2. What goes in the models folder, and what goes in the schemas folder?"

    Models hold the ORM/ODM classes that map data to the database (for example a Beanie `Document`). Schemas hold Pydantic classes that validate and serialize API input and output.

??? question "3. Why keep models and schemas separate?"

    It separates how data is stored from how it is exposed or received. Schemas can leave out sensitive or internal fields, or add output-only fields, without changing the stored model.
