# Release

This document outlines the components, target environments, deployment steps, licensing, and versioning strategy for the BookBuddy application.

## What to Release

A release of BookBuddy typically involves packaging the following components:

* **Backend Application:** Python Flask code, including routes, models, forms, and service logic.
* **Frontend Assets:** HTML templates (located in `Bookbuddy_app/Templates/`), CSS stylesheets, and JavaScript files (located in `Bookbuddy_app/static/`).
* **Dependencies:** The list of required Python packages specified in `requirements.txt`.
* **Database Migrations:** Scripts needed to update the database schema, if applicable for the release.
* **Configuration:** Secure management of sensitive details like `SECRET_KEY` and `GOOGLE_BOOKS_API_KEY` is critical. This is often handled through environment variables (potentially loaded via `python-dotenv` during development) and by ensuring configuration files containing secrets are listed in `.gitignore`.


## Licensing

### Current Status
 **Choice of the License:**
*   **Which one and why:** The project uses the **Apache License 2.0**, as specified in the `LICENSE` file and `README.md`. This is a permissive license that allows for broad use, modification, and distribution, while also providing patent protection and defining contribution terms. It's a common and well-regarded choice for open-source projects.



## Versioning Schema: Semantic Versioning (SemVer)

For Bookbuddy, Semantic Versioning (SemVer) is chosen because it offers a clear and widely adopted standard for managing releases. This schema makes it easy to communicate the impact of changes to developers and users, ensuring predictable updates and smoother integration with dependencies.

#### The versioning format follows the structure:

1. MAJOR: Incremented for backward-incompatible changes, such as replacing the authentication process, restructuring the database, or introducing breaking API changes.
2. MINOR: Incremented for backward-compatible new features or enhancements, like adding a new recommendation engine or improved search filters.
3. PATCH: Incremented for backward-compatible bug fixes or minor improvements, such as UI fixes, performance tuning, or resolving small backend issues.

This approach ensures that every release conveys the scale of change, allowing developers and users to upgrade with confidence.


