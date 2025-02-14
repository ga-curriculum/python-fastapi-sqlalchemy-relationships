<h1>
  <span class="headline">FastAPI SQLAlchemy Relationships</span>
  <span class="subhead">Update Seed Module</span>
</h1>

**Learning Objective:** By the end of this lesson, you will be able to **implement** an update to the seeding module to include related **Tea** data.

### Updating the `tea_data.py` File

In this lesson, we will update the `seed.py` file and the associated data file to seed both teas and related comments into the database. This process ensures that our database is pre-populated with meaningful test data.

The `tea_data.py` file contains the data we want to insert into the database. We will define both `TeaModel` and `CommentModel` instances and establish the relationship between them by specifying the `tea_id` for each comment.

```py
# data/tea_data.py
from models.tea import TeaModel
from models.comment import CommentModel

# List of teas to seed into the database
teas_list = [
    TeaModel(name="chai", rating=4, in_stock=True),
    TeaModel(name="earl grey", rating=3, in_stock=False),
    TeaModel(name="matcha", rating=3, in_stock=True),
    TeaModel(name="green tea", rating=5, in_stock=True),
    TeaModel(name="black tea", rating=4, in_stock=True),
    TeaModel(name="oolong", rating=4, in_stock=False),
    TeaModel(name="hibiscus", rating=4, in_stock=True),
    TeaModel(name="peppermint", rating=5, in_stock=True),
    TeaModel(name="jasmine", rating=3, in_stock=True)
]

# List of comments related to teas
# Each comment is associated with a tea using the tea_id
comments_list = [
    CommentModel(content="This is a great tea", tea_id=1),
    CommentModel(content="Perfect for relaxing evenings", tea_id=2),
    CommentModel(content="I love the vibrant green color!", tea_id=3),
    CommentModel(content="So refreshing and healthy!", tea_id=4),
    CommentModel(content="A classic choice for any time of day", tea_id=5)
]
```

### Updating the `seed.py` File

The `seed.py` file is responsible for inserting data into the database. It clears the existing database, recreates the tables, and inserts the new data.

```py
# seed.py
from sqlalchemy.orm import Session, sessionmaker
from data.tea_data import teas_list, comments_list
from config.environment import db_URI
from sqlalchemy import create_engine
from models.base import Base # import base model

engine = create_engine(db_URI)
SessionLocal = sessionmaker(bind=engine)

try:
    print("Recreating database...")
    # Drop and recreate tables to ensure a clean slate
    Base.metadata.drop_all(bind=engine)
    Base.metadata.create_all(bind=engine)

    print("Seeding the database...")
    db = SessionLocal()

    # Seed teas first, as comments depend on them
    db.add_all(teas_list)
    db.commit()

    # Seed comments after teas
    db.add_all(comments_list)
    db.commit()
    db.close()

    print("Database seeding complete! 👋")
except Exception as e:
    print("An error occurred:", e)
```

### Running the Seed Script

To run the seed script, execute the following command in your terminal:

```sh
pipenv run python seed.py
```

If everything is successful, you should see output indicating that the database has been recreated and seeded.

### Verifying the Data

To confirm that the data has been inserted correctly, use the `psql` tool to query the database.

```sh
psql -d teas_db -U <username>
```

### Query the Tables

```sql
-- View all teas
SELECT * FROM teas;

-- View all comments
SELECT * FROM comments;
```

You should see the following results:

1. The `teas` table contains the teas from `teas_list`.
2. The `comments` table contains the comments from `comments_list`, with the correct `tea_id` linking them to their respective teas.

## Next Steps

Well done! You have established a **1-to-Many (1:M)** data relationship and successfully reseeded your database to reflect this updated structure.

The next step involves implementing this relationship in your API routes. This will allow your application to handle operations that interact with both teas and their associated comments.

This functionality will be covered in a future lesson.
