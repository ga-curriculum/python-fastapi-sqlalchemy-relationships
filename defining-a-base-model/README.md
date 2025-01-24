<h1>
  <span class="headline">FastAPI SQLAlchemy Relationships</span>
  <span class="subhead">Defining a Base Model</span>
</h1>

**Learning Objective:**  
By the end of this lesson, learners will be able to **implement** a base model class for SQLAlchemy and understand its purpose in creating consistent, reusable models.

## Creating a Base Model

To begin, create a new module called `models/base.py`. This file will house logic that all our models can share.

```sh
touch models/base.py
```

### What is a SQLAlchemy Base Model?

A SQLAlchemy base model serves as a foundational template that other models inherit from. This allows all models to share common attributes and functionality, reducing code duplication and ensuring consistency across your application.

Here’s an example of what your `models/base.py` file might look like:

```py
# models/base.py
from sqlalchemy import Column, DateTime, Integer, func
from sqlalchemy.ext.declarative import declarative_base

# Create a base class for all models
Base = declarative_base()

class BaseModel(Base):
    __abstract__ = True  # Prevents this class from being mapped to a database table

    id = Column(Integer, primary_key=True, index=True)  # Unique identifier for each record
    created_at = Column(DateTime, default=func.now())  # Timestamp for when the record was created
    updated_at = Column(DateTime, default=func.now(), onupdate=func.now())  # Auto-updates on changes
```



Let’s break down the code to make it clearer:

1. **`Base = declarative_base()`**  
   This creates a base class that all models will inherit from. It serves as the foundation for defining SQLAlchemy models.

2. **`__abstract__ = True`**  
   The `__abstract__` attribute tells SQLAlchemy that this class is not tied to any database table. It exists purely to be inherited by other models.

3. **`id` column**  
   - The `id` field acts as the primary key for all models that inherit from `BaseModel`.  
   - Setting `primary_key=True` ensures each record has a unique identifier.  
   - The `index=True` improves query performance when filtering by `id`.

4. **`created_at` and `updated_at` columns**  
   - **`created_at`**: Automatically stores the timestamp when a record is first created.  
   - **`updated_at`**: Automatically updates whenever a record is modified.  
   - Both fields use `func.now()` from SQLAlchemy, which uses the database’s current timestamp function.


