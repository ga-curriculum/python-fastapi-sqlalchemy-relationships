<h1>
  <span class="headline">FastAPI SQLAlchemy Relationships</span>
  <span class="subhead">Defining a Comments Model</span>
</h1>

**Learning Objective:**  
By the end of this lesson, learners will be able to **define** a second, related SQLAlchemy model class for storing and managing comments data.

## Creating the comment model

In this lesson, we will create a `CommentModel` class to represent comments and their relationship to a tea. This will involve defining attributes for the comment and establishing a connection to the tea it references.

First, create a new file named `models/comment.py`.

```sh
touch models/comment.py
```

Inside this file, define the `CommentModel` class as shown below:

```py
# models/comment.py
from sqlalchemy import Column, Integer, String, ForeignKey
from sqlalchemy.orm import relationship
from .base import BaseModel

class CommentModel(BaseModel):

    __tablename__ = "comments"  # The name of the table in the database

    id = Column(Integer, primary_key=True, index=True)  # Unique identifier for the comment
    content = Column(String, nullable=False)  # The text content of the comment

    # ForeignKey establishes a connection to the teas table
    tea_id = Column(Integer, ForeignKey('teas.id'), nullable=False)
    tea = relationship("TeaModel", back_populates="comments")  # Defines the relationship to the TeaModel
```

The comment model specifies three attributes:

- A unique `id` for the comment (integer)
- The comment `content` (string)
- The `tea_id` that the comment pertains to (integer)

### What is a foreign key?

A **foreign key** is a special database constraint used to connect two tables. It ensures that a value in one table (like `tea_id` in the `comments` table) corresponds to a valid value in another table (like `id` in the `teas` table).

For example:

- If `tea_id` in a comment is `5`, then there must be a record in the `teas` table where `id` is `5`.
- This ensures that each comment always belongs to an existing tea.

> **Tip:** The string passed to `ForeignKey` must match the `__tablename__` of the related table and the name of its primary key. For example, `ForeignKey('teas.id')` links the `comments` table to the `id` column in the `teas` table.

With this model, you now have a structure to manage comments data and link it to teas in your application.
