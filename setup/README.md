<h1>
  <span class="headline">FastAPI SQLAlchemy Relationships</span>
  <span class="subhead">Setup</span>
</h1>

## Setup

In this lesson, we’ll start by working with a pre-existing application that utilizes a PostgreSQL database instance, SQLAlchemy models and a database seeded with initial data.

> If you have a complete, working application from the `Python FastAPI SQLAlchemy Models` Lesson, you may choose to use that codebase as starter code instead of the repo provided below.

### 1. Clone the starter code

We’ve provided a starter repository with the base application code. Clone the repository to your local machine and rename the folder for this lesson:

```bash
git clone https://git.generalassemb.ly/modular-curriculum-all-courses/python-fastapi-sqlalchemy-models-solution python-fastapi-sqlalchemy-relationships
cd python-fastapi-sqlalchemy-relationships
```

### 2. Install dependencies:

This project uses `pipenv` for managing dependencies. To install everything the project needs, run:

```sh
 pipenv install
```

### 3. Activate the virtual environment:

```sh
 pipenv shell
```

### 4. Set up the database

1. Set up your PostgreSQL database:

   - Ensure PostgreSQL is installed and running on your machine.
   - Create a database named `teas_db` if it does not already exist:

```bash
createdb teas_db
```

### 5. Connect to database

Open the application in Visual Studio Code:

```bash
code .
```

The database connection string is defined in the `config/environment.py` file:

```python
db_URI = "postgresql://<username>@localhost:5432/teas_db"
```

- Ensure your PostgreSQL instance is configured to allow connections with the provided credentials.
- **_Modify your database connection string to use your username as the `<username>`._**

### 6. Seed the database

Seed the database with initial data:

- Run the `seed.py` file to reset the database by dropping existing tables and repopulating it with starter data:

```bash
pipenv run python seed.py
```

> You should see output indicating the database was successfully seeded. If there are any errors, check the `db_URI` in the `config/environment.py` file.
