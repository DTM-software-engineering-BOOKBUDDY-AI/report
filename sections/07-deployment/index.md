---
title: Deployment
has_children: false
nav_order: 8
---

# Deployment

# Section 4: Deployment and Execution

## 4.1 Introduction

This section provides comprehensive instructions for setting up the necessary development environment and running the **Bookbuddy** book recommendation application locally from its source code repository. The primary goal is to enable users (such as developers, testers, course instructors, or TAs) who have access to the source code to execute the application on their own machine for evaluation, testing, or further development purposes.

These instructions focus exclusively on local setup and execution using Flask's built-in development server. They do not cover deployment to a production environment (e.g., cloud hosting platforms like Heroku, PythonAnywhere, AWS).

## 4.2 Prerequisites

Before beginning the setup process, please ensure that the following software components are installed and configured correctly on your system:

* **Python:** Version 3.8 or later is recommended, as the application was developed and tested using this version range. You can download Python from [https://www.python.org/](https://www.python.org/).
* **pip:** The Python package installer, used for managing project dependencies. Pip is typically included with modern Python installations. You can verify its installation by running `pip --version` in your terminal.
* **Git:** The distributed version control system required to clone the project repository. Git can be downloaded from [https://git-scm.com/](https://git-scm.com/).

## 4.3 Setup and Execution Steps

Please follow these steps sequentially in your terminal or command prompt to set up and run the Bookbuddy application:

**1. Clone the Repository:**

   First, obtain a local copy of the source code by cloning the Git repository. Replace `<your_repository_url>` with the actual HTTPS or SSH URL provided for the project repository.

   ```bash
   git clone <https://github.com/DTM-software-engineering-BOOKBUDDY-AI/Bookbuddy-coding-2025.git>

   cd <repository_directory_name>
   python -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt
   ```



# Bookbuddy Setup Guide

## 4.4 Install Dependencies

All required Python libraries for this project are specified in the `requirements.txt` file, located in the root of the repository. This includes critical packages like Flask (the web framework) and `python-dotenv` (for loading environment variables), among others. Install them using pip while the virtual environment is active:

```bash
pip install -r requirements.txt
```

## 4.5 Configure Environment Variables

The application requires a Google API Key, likely used for fetching book data or utilizing other Google services. This key must be provided securely through an environment variable rather than being hardcoded.

1. **Create a `.env` file**: In the root directory of the repository (the same directory containing `requirements.txt` and the `venv` folder), create a new file named exactly `.env`.

2. **Add the API Key**: Open the `.env` file with a plain text editor and add the following line, ensuring you replace `'YOUR_ACTUAL_GOOGLE_API_KEY'` with your valid Google API key obtained from Google Cloud Console or the relevant service:

   ```plaintext
   # .env file content
   GOOGLE_API_KEY='YOUR_ACTUAL_GOOGLE_API_KEY'
   ```

**Note**: The application utilizes the `python-dotenv` library (installed in the previous step) to automatically detect and load variables from the `.env` file when the application starts.

**Security Best Practice**: It is highly recommended to add the `.env` file to your project's `.gitignore` file. This prevents accidental commits of your secret API key to version control systems like Git. If a `.gitignore` file doesn't exist in the root directory, create one and add `.env` as a line item.

## 4.6 Navigate to the Application Directory

Based on the project structure, the main Flask application script (`app.py`) resides within a subdirectory named `Bookbuddy`. Change your current directory to this subdirectory:

```bash
cd Bookbuddy
```

**Assumption**: If your `app.py` is located directly in the repository root, you can skip this step. However, ensure the subsequent `python app.py` command is run from the correct location where `app.py` exists and where it can find `templates/static` files if applicable.

## 4.7 Run the Application

With the virtual environment active and positioned in the correct directory (`Bookbuddy`), start the Flask development server by executing the main application script:

```bash
python app.py
```

You should see output in the terminal indicating that the Flask server is running, usually including lines like:

- `* Environment: development`
- `* Debug mode: on/off`
- `* Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)`

### 4.8 Accessing the Application

Once the development server is running successfully, as indicated by the terminal output:

1. Open your preferred web browser (such as Chrome, Firefox, Safari, or Edge).
2. Enter the local address provided in the terminal into the browser's address bar. This is typically `http://127.0.0.1:5000/` or `http://localhost:5000/`.
3. The Bookbuddy application's home page should load, allowing you to interact with the book recommendation form.

### 4.9 Stopping the Application

To stop the local Flask development server when you are finished:

1. Return to the terminal window where the `python app.py` command is actively running.
2. Press `CTRL + C` (Control key and C key simultaneously).
3. The server will shut down, and control of the terminal prompt will be returned to you.
4. Optionally, you can deactivate the virtual environment by simply typing the command `deactivate` and pressing Enter.

By following these detailed steps, any user with the necessary prerequisites and access to the source code can successfully set up the environment, configure the required API key, and run the Bookbuddy application locally for testing, evaluation, or development purposes.
