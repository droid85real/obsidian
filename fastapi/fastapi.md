To run virtual environment 
+ `venv\Scripts\activate`

To run server 
+ `uvicorn app.main:app --reload`

To execute requirements.txt file
+ `pip install -r requirements.txt`






Basic folder structure

```
fastapi-app/
│── venv/                  # your virtual environment (don’t touch)
│── app/                   # main application folder
│   │── __init__.py        # makes "app" a Python package
│   │── main.py            # entry point (FastAPI app lives here)
│   │── routes/            # all your API routes
│   │   └── __init__.py
│   │   └── users.py       # example route file
│   │── models/            # database models (SQLAlchemy, Pydantic, etc.)
│   │   └── __init__.py
│   │── schemas/           # Pydantic request/response schemas
│   │   └── __init__.py
│   │── services/          # business logic (optional)
│   │   └── __init__.py
│   └── core/              # config, db connection, security utils
│       └── __init__.py
│
│── requirements.txt       # pinned dependencies
│── .gitignore             # if using git
```


### **Why `__init__.py`?**

- In Python, a folder with `__init__.py` is treated as a **package**.

- This allows you to **import files (modules) from that folder** just like you import libraries.

- Example: If you have
```
project/
│
├── main.py
└── blog/
    ├── __init__.py
    ├── models.py
    ├── routes.py
    ├── schemas.py
```

