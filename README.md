# FastAPI Blog — Setup & Run

This project is a small FastAPI application using SQLAlchemy and SQLite. This README explains how to create or use a virtual environment, install dependencies, run the app, open the interactive docs, and make example requests.

> Tested on macOS with zsh and Python 3.13 (adjust `python` commands for your environment).

## Prerequisites

- Python 3.10+ (project used 3.13)
- Git (optional if you cloned the repo)

## Quick start (recommended)

1. Open a terminal and change to the project directory:

   ```zsh
   cd "/Users/darshansiddarth/Documents/JOB prep/Fastapi"
   ```

2. Create a virtual environment (if you don't want to use the provided `blog-env`):

   ```zsh
   python3 -m venv blog-env
   source "$(pwd)/blog-env/bin/activate"
   ```

   If you already have the `blog-env` folder in the repo you can activate it:

   ```zsh
   source "./blog/blog-env/bin/activate"
   ```

3. Install dependencies from `requirements.txt`:

   ```zsh
   pip install -r requirements.txt
   ```

4. Run the FastAPI app with reload (development):

   ```zsh
   uvicorn blog.main:app --reload --port 8001
   ```

   - Default port is 8000; if it's already used, pass `--port 8001` (or another free port).
   - To stop the server press CTRL+C.

## Open the interactive API docs

- Swagger UI: http://127.0.0.1:8001/docs
- ReDoc: http://127.0.0.1:8001/redoc

These are generated automatically by FastAPI.

## Database

- The app uses SQLite and will create `blog.db` in the project directory when the app starts (SQLAlchemy `create_all` runs on startup).
- If you see a SQLAlchemy error about a missing referenced table (e.g. `NoReferencedTableError` for `users`), create a user first via the `/users` endpoint (examples below) so foreign keys succeed when creating blogs.

## Example requests

1. Create a user (POST /users)

   ```bash
   curl -X POST "http://127.0.0.1:8001/users" \
     -H "Content-Type: application/json" \
     -d '{"name":"alice","email":"alice@example.com","password":"secret"}'
   ```

   Response contains the user JSON including `id`.

2. Create a blog (POST /blog)

   - If no users exist the app creates a default user automatically. Otherwise the first user is used.

   ```bash
   curl -X POST "http://127.0.0.1:8001/blog" \
     -H "Content-Type: application/json" \
     -d '{"title":"My Post","body":"Hello world"}'
   ```

   Response contains the created blog JSON.

## Troubleshooting

- Address already in use:
  - Find process on default port and kill it:
    ```zsh
    lsof -i :8000
    kill -9 <PID>
    ```
  - Or run on a different port: `uvicorn blog.main:app --reload --port 8001`

- `ModuleNotFoundError: No module named 'sqlalchemy'`:
  - Activate the correct virtual environment and run `pip install -r requirements.txt` again.

- `sqlalchemy.exc.NoReferencedTableError` for `blogs.user_id`:
  - The `Blog` model has a foreign key to `users.id`. Create a user first via `/users` or ensure the `User` model is defined and `models.Base.metadata.create_all(bind=engine)` runs before creating blogs.

## Useful commands

- Activate venv (macOS / zsh):
  ```zsh
  source ./blog-env/bin/activate
  ```
- Install dependencies:
  ```zsh
  pip install -r requirements.txt
  ```
- Run server:
  ```zsh
  uvicorn blog.main:app --reload
  ```
- Run on different port:
  ```zsh
  uvicorn blog.main:app --reload --port 8001
  ```

## Notes

- The repository already contains `blog-env` in the `blog/` folder. If you prefer, create and use a fresh virtual environment outside the repo to keep dependencies isolated.
- For production, do not use `--reload` and consider a production-ready server config (gunicorn/uvicorn with workers) and a proper RDBMS.

If you want, I can also add Postman/HTTPie examples, or update README with environment variable instructions.  
