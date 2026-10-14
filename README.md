# Plateful — An e-Recipe Sharing Web Application

![CI](https://github.com/Brandonfzh/Plateful-AgileWD-Project-2026/actions/workflows/ci.yml/badge.svg)

> **Fork note (Brandon Fong):** This is my fork of the team project below. I added a GitHub Actions CI pipeline (`.github/workflows/ci.yml`) that runs the project's unit tests and Selenium end-to-end tests on every push and pull request.

## Context
The web application Plateful was created for a group project as part of the unit CITS3403/CITS5505: Agile Web Development at [The University of Western Australia](https://www.uwa.edu.au/home) during the first semester of 2026.

---

## Project Team

| Student Name      | Student Number | GitHub Username    |
|-------------------|----------------|--------------------|
| Brandon Fong      | 24339304       | Brandonfzh         |
| Annabelle Tiew    | 24028292       | icecreampuppy1231  |
| Kathleen Isabella | 24091081       | kathisabella       |
| Kaili Zhou        | 24057973       | KylieZhou          |

---

## About

Plateful is a web-based recipe-sharing platform that provides a seamless and enjoyable environment where users can create, share, discover, and interact with a wide variety of recipes. The platform focuses on the social and collaborative aspect of cooking — encouraging users to upload their own recipes and engage with others through ratings, comments, collections, and following.

---

## Python version

This project is built and tested with Python 3.12.

Python 3.14 is not recommended because some dependencies, such as `greenlet`, may not work correctly with the newest Python version.

---

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/kathisabella/Plateful-AgileWD-Project-2026.git
cd Plateful-AgileWD-Project-2026
```

### 2. Create and activate a virtual environment

This project should be run with Python 3.12.

**macOS / Linux**
```bash
python3.12 -m venv venv
source venv/bin/activate
```

**Windows (PowerShell)**
```powershell
py -3.12 -m venv venv
.\venv\Scripts\Activate.ps1
```

### 3. Install dependencies

```bash
python -m pip install -r requirements.txt
```

### 4. Set up environment variables

Create a `.env` file in the project root:

```
APP_SECRET_KEY=your-secret-key-here
```

`APP_SECRET_KEY` can be any random string for local development.

### 5. Set up the database

Run the database migrations:

```bash
flask --app app db upgrade
```

This will create `main/plateful.db`.

### 6. Seed demo data (optional)
To populate the database with demo users and recipes:

```bash
flask shell
```
```python
>>> from main.models import create_test_data
>>> create_test_data()
```
Exit shell:
```python
>>> exit()
```


Demo accounts created:

| Email | Password |
|---|---|
| demo@plateful.com | demo1234 |
| alice@plateful.com | alice1234 |
| ben@plateful.com | ben1234 |
| cara@plateful.com | cara1234 |

> Re-run `create_test_data()` at any time to reset the database back to the demo state.

### 7. Run the app

```bash
python app.py
```

### 8. Open in browser

```
http://127.0.0.1:5000
```

### 9. Stop the server

Press `Ctrl + C` to stop. Run `deactivate` to exit the virtual environment.

---

## Project Structure

```
Plateful-AgileWD-Project-2026/
├── app.py
├── CITS3403-User Stories.pdf
├── ERD
│   └── ERD_Plateful.png
├── .github
│   └── workflows
│       └── ci.yml           ← GitHub Actions CI (unit + Selenium tests)
├── main
│   ├── __init__.py          ← app factory, extension setup
│   ├── blueprints.py        ← Blueprint registration
│   ├── config.py            ← Config classes (Dev, Test, Selenium)
│   ├── extensions.py        ← Shared extension instances
│   ├── forms.py             ← WTForms form classes
│   ├── mealplanner.py       ← Meal planner helpers
│   ├── models.py            ← SQLAlchemy models
│   ├── routes.py            ← All route handlers
│   ├── static
│   │   ├── login.js
│   │   ├── profile.js
│   │   ├── recipe_form.js
│   │   ├── styles.css
│   │   └── uploads/         ← User-uploaded recipe images
│   └── templates
│       ├── 404.html
│       ├── base_auth.html
│       ├── base.html
│       ├── dashboard.html
│       ├── edit_recipe.html
│       ├── explore.html
│       ├── following.html
│       ├── forgot_password.html
│       ├── login.html
│       ├── mealplanner.html
│       ├── my_recipes.html
│       ├── privacy.html
│       ├── profile.html
│       ├── recipe_details.html
│       ├── saved_recipe.html
│       ├── settings.html
│       ├── terms.html
│       ├── upload_recipe.html
│       └── user_profile.html
├── tests
│   ├── test_unit.py         ← 24 unit tests (in-memory SQLite)
│   └── test_selenium.py     ← 21 Selenium end-to-end tests
├── Testing.md
├── README.md
└── requirements.txt
```

> The app uses a Blueprint-based Flask structure. The factory function lives in `main/__init__.py`, the Blueprint is registered in `main/blueprints.py`, and all route handlers are in `main/routes.py`.

> Database Notes:
> - SQLite is used for local development
> - Database file is ignored using `.gitignore`
> - Alembic/Flask-Migrate is used for schema migrations
> - Existing migrations are stored in: `migrations/versions/`

---

## Continuous Integration

On every push and pull request, GitHub Actions installs dependencies on Python 3.12, runs the unit tests (`tests/test_unit.py`), and then runs the Selenium end-to-end tests (`tests/test_selenium.py`) headless. See `.github/workflows/ci.yml`.

---

## Tech Stack

| Layer        | Technology                                        |
|--------------|---------------------------------------------------|
| Backend      | Python · Flask                                    |
| Database     | SQLite · SQLAlchemy · Flask-Migrate (Alembic)     |
| Forms        | Flask-WTF · WTForms (with CSRF protection)        |
| Auth         | Werkzeug password hashing · Flask sessions        |
| Rate Limiting| Flask-Limiter                                     |
| Frontend     | HTML · CSS · JavaScript                           |
| Templating   | Jinja2                                            |
| Fonts        | Google Fonts (Fraunces, Figtree)                  |
| CI           | GitHub Actions · pytest · Selenium                |
