<h1>
  <span class="headline">FastAPI SQLAlchemy Relationships</span>
  <span class="subhead">Update Model Data Relations</span>
</h1>

**Learning Objective:**  
By the end of this lesson, you will be able to **implement** model data relationships in a SQLAlchemy model.

## Updating the TeaModel to Relate to Comments

To link the `TeaModel` and `CommentModel`, we need to establish a relationship between these models. This involves updating the `TeaModel` to include a `comments` property that represents the relationship.

This property uses SQLAlchemy's `relationship` method to manage how the two tables (teas and comments) are connected in the database.

### Update `TeaModel`

Here’s the updated code for `TeaModel`:

```py
# models/tea.py
from sqlalchemy import Column, Integer, String, Boolean
from sqlalchemy.orm import relationship
from .base import BaseModel
from .comment import CommentModel  # Import CommentModel to reference it

class TeaModel(BaseModel):

    # Name of the table in the database
    __tablename__ = "teas"

    id = Column(Integer, primary_key=True, index=True)  # Unique identifier for teas

    # Specific columns for the Tea table
    name = Column(String, unique=True)  # Name of the tea (must be unique)
    in_stock = Column(Boolean)  # Whether the tea is in stock
    rating = Column(Integer)  # Rating of the tea

    # Relationship to the comments table
    comments = relationship("CommentModel", back_populates="tea")
```

Let’s break down the important updates:

1. **Importing `CommentModel`**

   - At the top of the file, we imported the `CommentModel`.
   - This allows us to reference it in the `relationship` method.

2. **Adding the `comments` Property**

   - The `comments` property is defined using SQLAlchemy’s `relationship` method.
   - This property links `TeaModel` to `CommentModel`, telling SQLAlchemy to manage their connection.

   ```py
   comments = relationship("CommentModel", back_populates="tea")
   ```

### Why Use back_populates?

The `back_populates` attribute ensures that the relationship works in both directions:

- In `TeaModel`: The comments property retrieves all comments related to a tea.
- In `CommentModel`: The tea property links back to the tea that a comment belongs to.

By defining back_populates in both models, we create a synchronized two-way connection.
