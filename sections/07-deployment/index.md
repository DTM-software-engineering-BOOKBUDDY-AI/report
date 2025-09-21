# Deployment   
**Deployment and Execution of bookbuddy**

## 4.1 Introduction  
This section provides clear instructions for setting up the development environment and running the **Bookbuddy** book recommendation application locally. The goal is to allow developers, testers, or instructors to execute the application on their own machines for testing, evaluation, or further development.  
Deployment focuses on **local execution** using Flask’s built-in development server. Production deployment (e.g., on Heroku, AWS, or Docker) is outside the scope of this section.

---

## 4.2 Technologies Used  
- **Backend**: Flask (Python)  
- **Frontend**: HTML, CSS, JavaScript (Jinja2 templates)  
- **Database**: SQLite (development), PostgreSQL (recommended for production)  
- **Server**: Flask development server  


## 4.3 System Requirements  
- Python 3.8 or later  
- pip (Python package manager)  
- Git (for cloning the repository)  
- (Optional) Virtual environment manager (venv) 
- 

## 4.2 Prerequisites

Before getting started, make sure you have the following tools installed:

* **Python:** Version 3.8 or later is recommended, as the application was developed and tested using this version range. You can download Python from [https://www.python.org/](https://www.python.org/).
* **pip:** The Python package installer, used for managing project dependencies. Pip is typically included with modern Python installations. You can verify its installation by running `pip --version` in your terminal.
* **Git:** The distributed version control system required to clone the project repository. Git can be downloaded from [https://git-scm.com/](https://git-scm.com/).

---

# 4.5 Setup and Execution Steps  

###  Step 1: Clone the repository
First, obtain a local copy of the source code by cloning the Git repository. Replace <your_repository_url> with the actual HTTPS or SSH URL provided for the project repository.
```bash
git clone https://github.com/DTM-software-engineering-BOOKBUDDY-AI/Bookbuddy-coding-2025.git
cd Bookbuddy-coding-2025 
```


### Step 2: Create and activate a virtual environment
```bash
python -m venv venv
# macOS/Linux
source venv/bin/activate
# Windows
venv\Scripts\activate
```

### Step 3: Install dependencies
All required libraries are listed in requirements.txt (root folder), including `Flask` and `python-dotenv`. Install them with `pip` inside the active virtual environment.
```bash 
pip install -r requirements.txt
```
### Step 4: Configure environment variables
1. **Create a `.env` file**: In the root directory of the repository (the same directory containing `requirements.txt` and the `venv` folder), create a new file named exactly `.env`.

2. **Add the API Key**: Open the `.env` file with a plain text editor and add the following line, ensuring you replace `'YOUR_ACTUAL_GOOGLE_API_KEY'` with your valid Google API key obtained from Google Cloud Console or the relevant service:

```bash
GOOGLE_API_KEY='YOUR_ACTUAL_GOOGLE_API_KEY'
```
⚠️ Add .env to .gitignore to protect sensitive keys.

### Step 5: Navigate to the application directory
If the main script is located inside a subdirectory:
```bash
cd Bookbuddy
```
### Step 6 : Run the application
With the virtual environment active and positioned in the correct directory (Bookbuddy), start the Flask development server by executing the main application script:
```bash
python app.py
```
output should be :
```bash
* Environment: development
* Debug mode: on/off
* Running on http://127.0.0.1:5000/
```

### Step 7: Access the application
**Open a browser and go to**  http://127.0.0.1:5000/   **to use Bookbuddy**
The Bookbuddy application's home page should load, allowing you to interact with the book recommendation form.

### Step 8: Stop the application
Press CTRL + C in the terminal.
Deactivate the virtual environment with:
```bash
deactivate
```

>By following these detailed steps, any user with the necessary prerequisites and access to the source code can successfully set up the environment, configure the required API key, and run the Bookbuddy application locally for testing, evaluation, or development purposes.


