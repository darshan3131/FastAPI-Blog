
<h1 align="center">📖 FastAPI Blog</h1>  
<h3 align="center">A lightweight blogging API built with FastAPI, SQLAlchemy & SQLite</h3>  


<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10%2B-blue?logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/FastAPI-0.110+-teal?logo=fastapi&logoColor=white" />
  <img src="https://img.shields.io/badge/Database-SQLite-lightgrey?logo=sqlite&logoColor=blue" />
  <img src="https://img.shields.io/badge/ORM-SQLAlchemy-red?logo=python&logoColor=white" />
</p>  




🚀 Features
	•	📝 Create and manage blogs
 
	•	👤 User registration with password hashing
 
	•	🔗 Blogs linked to users via foreign keys
 
	•	📂 SQLite database (auto-generated on startup)
 
	•	⚡ Interactive API docs via Swagger UI and ReDoc
 


⚙️ Tech Stack
	•	Backend: FastAPI
	•	ORM: SQLAlchemy
	•	Database: SQLite
	•	Server: Uvicorn


🛠️ Setup & Run
	1.	Clone the repository:
git clone https://github.com/darshan3131/FastAPI-Blog.git
cd FastAPI-Blog


	2.	Create and activate a virtual environment:
python3 -m venv blog-env
source blog-env/bin/activate


	3.	Install dependencies:
pip install -r requirements.txt


	4.	Run the app:
uvicorn blog.main:app --reload --port 8001


	5.	Open API Docs:
	•	Swagger UI → http://127.0.0.1:8001/docs
	•	ReDoc → http://127.0.0.1:8001/redoc



🗄️ Database
	•	Uses SQLite (blog.db) created automatically on startup.
	•	Note: A blog must be linked to a user. Create a user first via /users.


📌 Example Requests

Create a user
curl -X POST "http://127.0.0.1:8001/users" \
  -H "Content-Type: application/json" \
  -d '{"name":"alice","email":"alice@example.com","password":"secret"}'

Create a blog
curl -X POST "http://127.0.0.1:8001/blog" \
  -H "Content-Type: application/json" \
  -d '{"title":"My Post","body":"Hello world"}'



🐛 Troubleshooting
	Port already in use → run on another port:

uvicorn blog.main:app --reload --port 8002


	Missing dependencies → reinstall:

pip install -r requirements.txt



📂 Project Structure

```bash
FastAPI-Blog/
│── blog/
│   ├── __init__.py
│   ├── main.py           # Entry point for FastAPI app
│   ├── database.py       # Database connection & session
│   ├── models.py         # SQLAlchemy models (User, Blog, etc.)
│   ├── schemas.py        # Pydantic schemas for validation
│   │
│   ├── routers/          # Routers for different features
│   │   ├── __init__.py
│   │   ├── user.py       # Endpoints for user CRUD
│   │   ├── blog.py       # Endpoints for blog CRUD
│   │
│   ├── repository/       # Data access layer (CRUD logic)
│   │   ├── __init__.py
│   │   ├── user.py
│   │   ├── blog.py
│   │
│   ├── utils/            # Helpers (hashing, auth, etc.)
│       ├── __init__.py
│       ├── hashing.py    # Password hashing with bcrypt
│       ├── oauth2.py     # JWT authentication (future upgrade)
│
│── requirements.txt
│── README.md


⸻

🌟 Future Enhancements
	•	🔑 JWT Authentication
	•	🗄️ Migrate to PostgreSQL/MySQL
	•	🧑‍💻 Role-based permissions
	•	🚀 Docker support

⸻

And at the end you can keep your enhancements:

```markdown
✨ **Future Enhancements**
- 🔑 JWT Authentication  
- 🛢️ Migrate to PostgreSQL/MySQL  
- 👨‍💻 Role-based permissions  
- 🚀 Docker support  

⚡ Built with ❤️ using FastAPI



⸻
