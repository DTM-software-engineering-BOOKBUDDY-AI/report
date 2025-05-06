---
title: Development
has_children: false
nav_order: 5
---

# Development
This section outlines the version control practices employed during the project and discusses a key learning experience related to project setup.
## Development



### Implementation Details

-   **Network Protocols:**
    -   **HTTP/S (Hypertext Transfer Protocol Secure):** Used for all primary communication.
        -   **Client (Browser) <-> Flask Server:** Standard web communication for requesting pages and submitting data. HTTPS should be enforced in production for security.
        -   **Flask Server -> Google Books API:** Used to interact with the external REST API over the internet securely.
    -   **TCP (Transmission Control Protocol):** The underlying transport protocol for HTTP/S, ensuring reliable, ordered data delivery.
    -   **Why?** HTTP is the standard protocol for the web, suitable for the request/response nature of this application. HTTPS adds a necessary layer of security for data in transit. TCP provides the reliability needed for HTTP communication.

-   **In-transit Data Representation:**
    -   **HTML (HyperText Markup Language):** Sent from the Flask server to the client browser to render web pages.
    -   **JSON (JavaScript Object Notation):**
        -   Used for communication between the Flask server and the Google Books API.
        -   Used for internal AJAX requests (e.g., `/add-to-reading-list` endpoint expects JSON).
    -   **URL-encoded Form Data:** Sent from the browser to the Flask server when submitting standard HTML forms (processed by Flask-WTF).
    -   **Why?** HTML/CSS/JS are standard web frontend technologies. JSON is lightweight, human-readable, and the de facto standard for APIs (like Google Books) and modern web application communication (AJAX). Form data is the traditional way HTML forms submit data.

-   **Database Querying:**
    -   **SQL (Structured Query Language):** Used implicitly via an ORM.
    -   **SQLAlchemy (Object-Relational Mapper):** This library is used to interact with the database. Developers write Python code to define models and query data using Python objects and methods (e.g., `User.query.filter_by(...)`). SQLAlchemy translates these operations into SQL queries specific to the configured database dialect (SQLite, PostgreSQL, etc.).
    -   **Why?** SQL is the standard language for relational databases. SQLAlchemy provides a Pythonic way to interact with the database, abstracting away raw SQL, improving developer productivity, and reducing the risk of SQL injection vulnerabilities (when used correctly). It also allows for easier switching between different relational database backends.

-   **Component Authentication:**
    -   **Flask Server (User Authentication):** Uses **Flask-Login**.
        -   Initial authentication is done via username/password verification (`check_password_hash` in the `User` model).
        -   Subsequent requests are authenticated using **secure session cookies** managed by Flask-Login, which identify the logged-in user.
    -   **Flask Server -> Google Books API:** Uses an **API Key** (`GOOGLE_BOOKS_API_KEY` in `config.py`, passed as a query parameter in requests made by `services/google_books.py`).
    -   **Why?** Session cookies are a standard and relatively simple way to manage user login state in traditional web applications. API Keys are a common method for authenticating application access to external APIs like Google Books.

-   **Component Authorization:**
    -   **Flask Server (User Authorization):**
        -   **Login Requirement:** Flask-Login's `@login_required` decorator restricts access to certain routes (e.g., `/my_lib`, `/profile`, `/form`) to authenticated users only.
        -   **Profile Privacy:** A simple check (`user.privacy == 'private'`) combined with checking if the viewer is the owner (`current_user.id != user.id`) restricts access to private profiles.
    -   **Implicit Role-Based Access Control (RBAC):** The system implicitly defines roles like "Anonymous User", "Logged-in User", and "Profile Owner", granting different permissions based on these roles (e.g., only logged-in users can access `/my_lib`).
    -   **Why?** `@login_required` is a straightforward way provided by Flask-Login to protect endpoints. The privacy check implements a basic access control rule specific to the application's domain. This level of authorization is sufficient for the current features. More complex scenarios might necessitate more formal RBAC or Attribute-Based Access Control (ABAC) libraries.

### Technological Details

-   **Programming Languages, Frameworks, Libraries, Tools:**
    -   **Python:** Backend programming language. (Why: Widely used, large ecosystem, good framework support like Flask).
    -   **Flask:** Backend microframework for Python. (Why: Lightweight, flexible, extensible, suitable for building web applications and APIs).
    -   **HTML/CSS/JavaScript:** Frontend languages for structuring, styling, and adding interactivity to web pages. (Why: Standard web technologies).
    -   **SQLAlchemy:** Python SQL toolkit and Object-Relational Mapper. (Why: Simplifies database interaction, ORM benefits).
    -   **Flask-Login:** Flask extension for user session management (login, logout, remembering users). (Why: Integrates well with Flask, handles common authentication tasks).
    -   **Flask-WTF:** Flask extension for handling web forms (integration with WTForms). (Why: Simplifies form creation, validation, and CSRF protection).
    -   **Werkzeug:** WSGI utility library (used by Flask). (Why: Provides core components for request/response handling, routing).
    -   **Jinja2:** Templating engine for Python (used by Flask). (Why: Powerful, widely used for rendering dynamic HTML).
    -   **requests:** Python library for making HTTP requests. (Why: Standard and easy-to-use library for interacting with external APIs like Google Books).
    -   **scikit-learn:** Machine learning library for Python. (Why: Used for TF-IDF vectorization and cosine similarity calculation in the recommendation engine).
    -   **pandas/numpy:** Libraries for data manipulation and numerical operations. (Why: Often prerequisites or complementary tools for libraries like scikit-learn).
    -   **python-dotenv:** Reads key-value pairs from `.env` files. (Why: Standard practice for managing environment variables and secrets).
    -   **cachetools:** Extensible memoizing collections and decorators. (Why: Used for simple in-memory caching of Google Books API results).
    -   **pytest:** Testing framework for Python. (Why: Popular, powerful, and flexible testing tool).

-   **Key Dependencies (from `requirements.txt`):**
    -   `Flask`: Core web framework.
    -   `Flask-SQLAlchemy`: Database ORM integration.
    -   `Flask-Migrate`: Handles database schema migrations (using Alembic).
    -   `Flask-Login`: User authentication and session management.
    -   `Flask-WTF` / `WTForms` / `email-validator`: Form handling and validation.
    -   `Werkzeug`: WSGI utilities (Flask dependency).
    -   `requests`: HTTP client for Google Books API.
    -   `google-api-python-client`: (Listed, but `requests` seems to be used directly in `services/google_books.py`. Might be intended for other Google APIs or an alternative implementation).
    -   `scikit-learn` / `pandas` / `numpy`: Recommendation engine core logic (TF-IDF, similarity).
    -   `python-dotenv`: Loading configuration from `.env`.
    -   `cachetools`: Caching API results.
    -   `pytest` / `pytest-cov`: Testing and coverage reporting.
    -   `bleach`: HTML sanitization (likely for user-generated content like bios, though usage wasn't explicitly seen in reviewed files).
    -   `Flask-Talisman`: Security headers for Flask applications.
    -   `Flask-Limiter`: Rate limiting for Flask routes.

-   **Other External Technology/Service Dependencies:**
    -   **Google Books API:** Primary external service dependency. (Why: Provides the core book data for search, details, and potentially recommendations).
    -   **Goodreads API:** Mentioned in `README.md` but usage not confirmed in the reviewed code. (Why: Potentially for additional book data, reviews, or social features).

## Version Control (Git & GitHub)

The project utilized **GitHub** as its distributed version control system (DVCS) platform. Our workflow integrated task management using **Trello**, where a product backlog was maintained. Team members would select a task from the backlog and move it to their personal progress column. A key principle, similar to Scrum methodologies, was limiting Work In Progress (WIP): members focused on completing their current task before taking on a new one.

Key conventions included:

* **Branching Strategy:**
    * We employed a feature branching strategy. Each new feature or bug fix was developed in its own dedicated branch, created from the `main` branch.
    * Branch naming followed conventions like `feature/<feature-description>` (e.g., `feature/recommendation_system`) or `fix/<area>-<issue-description>` (e.g., `fix/mylib-database`).
    * To maintain repository cleanliness, feature and fix branches were deleted immediately after their corresponding code was successfully merged into the `main` branch.

* **Commit Conventions:**
    * While no strict commit message format (like Conventional Commits) was enforced, we aimed for descriptive messages. Each commit message typically summarized the changes made and indicated the part of the application affected.

* **.gitignore Usage:**
    * A `.gitignore` file was used to prevent specific files and directories from being tracked by Git. This primarily included the Python virtual environment directory (`venv`) and the `.env` file containing sensitive information like API keys.

## Implementation Details & Learning

One notable challenge encountered, which served as a practical learning experience, involved the initial setup of the `.gitignore` file.

### Challenge & Learning: Initial `.gitignore` Setup

* **The Problem:** We initially forgot to create and configure the `.gitignore` file *before* creating the Python virtual environment (`venv`) and making our first commits.
* **The Consequence:** As a result, the entire `venv` directory, containing numerous library files, was inadvertently committed to the repository.
* **The Impact:** This oversight wasn't noticed until later in the project. While not a critical application-breaking issue, committing the virtual environment added unnecessary bloat to the repository history and had the potential to cause confusion or unexpected behavior if different developers had slightly different environment setups.
* **The Learning/Recommendation:** This highlighted the importance of establishing the `.gitignore` file as one of the very first steps in a new project, *before* initializing dependencies or virtual environments. Configuring it correctly from the start prevents irrelevant or sensitive files from ever entering the version control history, leading to a cleaner and more manageable repository.




