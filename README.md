# Expand your team with Copilot coding agent

<img src="https://octodex.github.com/images/Professortocat_v2.png" align="right" height="200px" />

Hey alexandre-croteau!

Mona here. I'm done preparing your exercise. Hope you enjoy! 💚

Remember, it's self-paced so feel free to take a break! ☕️

[![](https://img.shields.io/badge/Go%20to%20Exercise-%E2%86%92-1f883d?style=for-the-badge&logo=github&labelColor=197935)](https://github.com/alexandre-croteau/skills-expand-your-team-with-copilot/issues/1)

---

## About This Repository

This repository contains the **Mergington High School Extracurricular Activities** web application — a full-stack app that lets students browse and sign up for after-school clubs and activities.

### Tech Stack

| Layer | Technology |
|-------|-----------|
| Backend | Python + [FastAPI](https://fastapi.tiangolo.com/) |
| Database | [MongoDB](https://www.mongodb.com/) (local instance) |
| Frontend | HTML, CSS, vanilla JavaScript |
| Auth | [Argon2](https://github.com/hynek/argon2-cffi) password hashing |
| Dev environment | GitHub Codespaces / VS Code |

### Repository Structure

```
.
├── src/
│   ├── app.py                  # FastAPI application entry point
│   ├── requirements.txt        # Python dependencies
│   ├── backend/
│   │   ├── database.py         # MongoDB setup and initial seed data
│   │   └── routers/
│   │       ├── activities.py   # Activity API endpoints
│   │       └── auth.py         # Teacher authentication endpoints
│   └── static/
│       ├── index.html          # Main web page
│       ├── app.js              # Frontend logic
│       └── styles.css          # Styling
├── docs/
│   └── how-to-develop.md       # Detailed development guide
└── .devcontainer/              # Codespaces configuration
```

### Getting Started

1. **Install dependencies**

   ```bash
   pip install -r src/requirements.txt
   ```

2. **Start MongoDB** (handled automatically in Codespaces; run manually if needed)

   ```bash
   ./.devcontainer/startMongoDB.sh
   ```

3. **Run the application**

   ```bash
   python -m uvicorn src.app:app --host 0.0.0.0 --port 8000
   ```

4. **Open the app** at `http://localhost:8000`
   - Interactive API docs: `http://localhost:8000/docs`

> In **GitHub Codespaces**, steps 1–2 are performed automatically on container creation. Use the VS Code *Run and Debug* panel (F5) with the **"Launch Mergington WebApp"** configuration to start the server.

### Key Concepts

#### Activities

Activities are stored in the `activities` MongoDB collection inside the `mergington_high` database. Each document uses the activity name as its `_id` and contains:

| Field | Type | Description |
|-------|------|-------------|
| `description` | string | Short description of the activity |
| `schedule` | string | Human-readable schedule (e.g. `"Tuesdays, 7:00 PM - 8:00 PM"`) |
| `schedule_details` | object | Structured schedule: `days[]`, `start_time`, `end_time` (24-hour) |
| `max_participants` | number | Maximum number of students allowed |
| `participants` | array | List of student email addresses currently enrolled |

Initial seed data is defined in `src/backend/database.py` and is loaded when the database is empty.

#### Adding a New Activity

Add a new entry to the `initial_activities` dictionary in `src/backend/database.py`:

```python
"My New Club": {
    "description": "A short description of the club.",
    "schedule": "Wednesdays, 3:30 PM - 4:30 PM",
    "schedule_details": {
        "days": ["Wednesday"],
        "start_time": "15:30",
        "end_time": "16:30"
    },
    "max_participants": 20,
    "participants": []
}
```

> The seed data is only loaded when the database collection is **empty**. Clear the collection (or restart with a fresh database) to see new seed entries.

#### Authentication

Teacher accounts are defined in `initial_teachers` in `src/backend/database.py`. Teachers must log in before they can register or unregister students. Passwords are hashed with Argon2.

### API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/activities` | List all activities with participant counts |
| `POST` | `/activities/{name}/signup` | Sign a student up for an activity |
| `DELETE` | `/activities/{name}/signup` | Remove a student from an activity |

See `http://localhost:8000/docs` for full interactive API documentation.

---

&copy; 2025 GitHub &bull; [Code of Conduct](https://www.contributor-covenant.org/version/2/1/code_of_conduct/code_of_conduct.md) &bull; [MIT License](https://gh.io/mit)

