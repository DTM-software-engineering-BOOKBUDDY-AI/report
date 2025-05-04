

# Developer Guide

This guide is intended for developers who want to contribute to the Bookbuddy project or extend its functionality.

## Development Environment Setup

### Prerequisites
- Python 3.8 or higher
- pip package manager
- Git version control
- PostgreSQL database
- Redis (optional, for caching)
- Node.js and npm (for frontend development)

### Setting Up the Development Environment

1. **Clone the Repository**
   ```bash
   git clone https://github.com/DTM-software-engineering-BOOKBUDDY-AI/Bookbuddy-coding-2025.git
   cd Bookbuddy-coding-2025
   ```

2. **Create and Activate Virtual Environment**
   ```bash
   python -m venv venv
   # On Windows
   venv\Scripts\activate
   # On macOS/Linux
   source venv/bin/activate
   ```

3. **Install Dependencies**
   ```bash
   pip install -r requirements.txt
   # For testing dependencies
   pip install -r requirements-test.txt
   ```

4. **Database Setup**
   ```bash
   # Configure local PostgreSQL
   python Bookbuddy/manage.py migrate
   python Bookbuddy/manage.py createsuperuser
   ```

5. **Run the Development Server**
   ```bash
   python Bookbuddy/manage.py runserver
   ```

## Project Structure

### Backend (Python)
- **Bookbuddy/** - Main project folder
  - **models/** - Database models and ORM
  - **views/** - View controllers
  - **templates/** - HTML templates
  - **static/** - Static files (CSS, JS, images)
  - **api/** - API endpoints
  - **utils/** - Utility functions
  - **migrations/** - Database migrations

### Testing
- **tests/** - Test directory
  - **unit/** - Unit tests
  - **integration/** - Integration tests
  - **fixtures/** - Test fixtures
  - **mocks/** - Mock objects

## Development Workflow

### Branching Strategy
1. **Feature Branches**
   - Create a new branch for each feature
   - Name format: `feature/feature-name`
   - Ex: `feature/book-recommendation`

2. **Bug Fix Branches**
   - Create a new branch for each bug fix
   - Name format: `fix/bug-description`
   - Ex: `fix/login-validation`

3. **Release Branches**
   - Created from develop for release preparation
   - Name format: `release/version-number`
   - Ex: `release/1.2.0`

### Pull Request Process
1. Create a pull request from your branch to the `main` branch
2. Ensure CI/CD pipeline passes
3. Request code review from at least one team member
4. Address reviewer comments
5. Merge once approved

## Coding Standards

### Python
- Follow PEP 8 style guide
- Maximum line length: 100 characters
- Use docstrings for functions and classes
- Write descriptive variable and function names

### HTML/CSS
- Follow BEM methodology for CSS
- Maintain responsive design principles
- Ensure accessibility compliance (WCAG 2.1)

### JavaScript
- Follow Airbnb JavaScript Style Guide
- Use ES6+ features
- Document functions and components

## Testing Guidelines

### Unit Testing
- Use pytest for unit testing
- Aim for at least 80% code coverage
- Test each function for expected behavior
- Include edge cases and error conditions

### Integration Testing
- Test component interactions
- Ensure database operations work correctly
- Verify API endpoints functionality

### Running Tests
```bash
# Run all tests
python -m pytest

# Run specific test file
python -m pytest tests/unit/test_models.py

# Run tests with coverage
python -m pytest --cov=Bookbuddy
```

## API Documentation

### Authentication
- API uses token-based authentication
- Request tokens via `/api/token/`
- Include token in header: `Authorization: Token <token_value>`

### Endpoints
- `/api/books/` - List and create books
- `/api/books/{id}/` - Retrieve, update, delete book
- `/api/users/` - User management
- `/api/recommendations/` - Book recommendations

### Response Format
All API responses follow this format:
```json
{
  "status": "success",
  "data": {
    // Response data here
  },
  "message": "Optional message"
}
```

## Troubleshooting

### Common Issues

1. **Database Connection Errors**
   - Verify PostgreSQL is running
   - Check connection credentials
   - Ensure migrations are applied

2. **Dependency Issues**
   - Update virtualenv: `pip install -r requirements.txt --upgrade`
   - Check for conflicting packages

3. **Testing Failures**
   - Ensure test database is configured
   - Verify fixtures are properly loaded
   - Check for environment-specific issues

## Contribution Guidelines

1. **Before Contributing**
   - Check existing issues and pull requests
   - Discuss major changes in an issue first
   - Review the documentation

2. **Contribution Process**
   - Fork the repository
   - Create a branch for your changes
   - Follow coding standards
   - Include appropriate tests
   - Update documentation
   - Submit a pull request

3. **Code Review**
   - All code requires review before merging
   - Address reviewer comments promptly
   - Be open to feedback and suggestions
