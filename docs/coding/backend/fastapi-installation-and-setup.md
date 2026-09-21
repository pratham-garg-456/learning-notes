---
title: FastAPI Installation and Setup
---

# FastAPI Installation and Setup

## Requirements

The [latest Python version](https://www.python.org/), or the version mentioned on the [FastAPI website](https://fastapi.tiangolo.com/#requirements).

## Installation

### Set up a virtual environment to install and run FastAPI

Docs: [creating virtual environments](https://docs.python.org/3/library/venv.html#creating-virtual-environments)

```bash
# use the path where your project is
python -m venv /path/to/new/virtual/environment

# Example: this creates a folder for the virtual environment named venv
python -m venv venv
```

### Activate the virtual environment

`<venv>` must be replaced by the path to the directory containing the virtual environment.

```powershell
# Example
venv\Scripts\Activate.ps1
```

!!! tip
    Make sure you see `venv` in front of your shell prompt.

### Install FastAPI

```bash
pip3 install fastapi
```

Or:

```bash
pip install "fastapi[standard]"
```

!!! tip
    The second method does not require you to install `uvicorn` (next step), because `standard` comes with it, and you can simply run the app using `fastapi dev main.py`.

### Install [uvicorn](https://www.uvicorn.org/)

```bash
pip3 install uvicorn
```

## Setup

Docs: [first steps](https://fastapi.tiangolo.com/tutorial/first-steps/)

Create `main.py`. Either a regular function:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def index(): # you can name it anything: root, broot, whatever
    return {"message": "Hello, World!"}
```

Or an async function:

```python
# main.py
from fastapi import FastAPI

app = FastAPI()


@app.get("/")
async def root():
    return {"message": "Hello World"}
```

!!! tip "Regular function vs async function"
    The first approach uses a regular function, the second an `async` function.

    **Regular function:** use when your function doesn't need to wait for databases, file operations, or external APIs.

    **Async function:** use when you plan to add database calls, file operations, or API calls later.

## Run the app

```bash
uvicorn main:app --reload
# When running with Uvicorn, if the instance name is app then use main:app,
# if it is myApp then use main:myApp. You can name it anything but it must match here.
```

Or:

```bash
fastapi dev main.py
```

## Practice Questions

??? question "1. Why create a virtual environment, and how do you activate it on Windows PowerShell?"

    It keeps the project's Python packages isolated. Create it with `python -m venv venv` and activate it with `venv\Scripts\Activate.ps1`. You should see `venv` in front of your shell prompt.

??? question "2. What is the difference between pip install fastapi and pip install fastapi[standard]?"

    The `standard` install includes `uvicorn`, so you don't need to install it separately and can run the app with `fastapi dev main.py`.

??? question "3. When should a route function be regular, and when async?"

    Regular when it doesn't need to wait for databases, file operations, or external APIs. Async when you plan to add database calls, file operations, or API calls.

??? question "4. What does uvicorn main:app --reload mean?"

    Run the `app` instance found in `main.py`, and reload automatically when the code changes. The name after the colon must match the name of your FastAPI instance (`main:myApp` if it is called `myApp`).
