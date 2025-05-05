---
title: Development
has_children: false
nav_order: 5
---

# Development
This section outlines the version control practices employed during the project and discusses a key learning experience related to project setup.

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
