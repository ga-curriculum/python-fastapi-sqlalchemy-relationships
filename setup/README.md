<h1>
  <span class="headline">FastAPI SQLAlchemy Relationships</span>
  <span class="subhead">Setup</span>
</h1>

## Setup

Open your Terminal application and navigate to your **`~/development/lessons`** directory:

```bash
cd ~/development/lessons
```

Make a new directory called **`sql-alchemy-data-relations`**, then enter this directory:

```bash
mkdir sql-alchemy-data-relations
cd sql-alchemy-data-relations
```

You may continue working with your existing FastAPI app - or copy the contents of the `lesson-starter` folder into the new `sql-alchemy-data-relations` directory.

Install the pipenv dependencies and start the development server

```bash
pipenv install
```

If you are starting this module without an existing `teas_db` - run the following commands

```bash
# dropdb teas_db # use this command if db errors occur when attempting to seed
createdb teas_db
pipenv run python seed.py
```

Open the contents of the directory in VSCode:

```bash
code .
```
