# BookBuddy Design Documentation

## Architecture

### System Components
BookBuddy follows a layered architecture pattern with the following main components:

mermaid
graph TD  
    A [Presentation Layer] --> B [Application Layer]
    B --> C[Domain Layer]
    C --> D[Data Layer]
    subgraph Presentation Layer
        E[Templates/HTML] --> F[Static Files]
        F --> G[JavaScript]
    end
    subgraph Application Layer
        H[Routes] --> I[Forms]
        I --> J[Services]
    end
    subgraph Domain Layer
        K[Models] --> L[Business Logic]
    end
    subgraph Data Layer
        M[Database] --> N[External APIs]
    end


### Component Details
1. **Presentation Layer**
    - Templates (`/templates`): HTML templates using Jinja2
    - Static files (`/static`): CSS, JavaScript, images
    - Client-side logic for user interactions

2. **Application Layer**
    - Routes (`app.py`, `routes/books.py`): Handle HTTP requests
    - Forms (`forms.py`): User input validation
    - Services (`services/google_books.py`): External service integration

3. **Domain Layer**
    - Models (`models.py`): Core business entities
    - Business Logic: Reading list management, book tracking

4. **Data Layer**
    - SQLite Database: Data persistence
    - Google Books API: External book data

## Modelling

### Core Domain Models

mermaid
classDiagram
User "1" -- "" ReadingList
ReadingList "" -- "1" Book
User "1" -- "1" UserPreferences
class User {
+id: Integer
+email: String
+username: String
+password_hash: String
+created_at: DateTime
+profile_picture: String
+bio: Text
+get_reading_lists()
+check_password()
}
class ReadingList {
+id: Integer
+user_id: Integer
+book_id: String
+status: String
+progress: Integer
+started_at: DateTime
+finished_at: DateTime
}
class Book {
+id: String
+title: String
+author: String
+cover_image: String
+genre: String
+language: String
+publication_year: Integer
+summary: Text
}
class UserPreferences {
+user_id: Integer
+favorite_genres: List
+preferred_language: String
+reading_goal: Integer
}


## Interaction

### Book Addition Sequence
mermaid
sequence diagram
participant U as User
participant C as Client
participant S as Server
participant GB as Google Books API
participant DB as Database
U->>C: Search for book
C->>S: GET /search?q={query}
S->>GB: Search request
GB-->>S: Book results
S-->>C: Display results
U->>C: Add to reading list
C->>S: POST /add-to-reading-list
S->>DB: Save book & list entry
DB-->>S: Confirm save
S-->>C: Success response
C-->>U: Update UI

## Behavior

### Reading List State Machine
mermaid
state diagram-v2
[] --> WantToRead
WantToRead --> CurrentlyReading: Start Reading
CurrentlyReading --> Finished: Complete
CurrentlyReading --> WantToRead: Pause
Finished --> WantToRead: Read Again
Finished --> []: Remove


## Data-Related Aspects

### Database Schema

#### Users Table
SQL
CREATE TABLE user (
id INTEGER PRIMARY KEY AUTOINCREMENT,
email VARCHAR(120) UNIQUE NOT NULL,
username VARCHAR(80) UNIQUE NOT NULL,
password_hash VARCHAR(128),
created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
profile_picture VARCHAR(200),
bio TEXT
);


#### Books Table
SQL
CREATE TABLE book (
id VARCHAR(20) PRIMARY KEY,
title VARCHAR(200) NOT NULL,
author VARCHAR(200) NOT NULL,
cover_image VARCHAR(500),
genre VARCHAR(100),
language VARCHAR(50),
publication_year INTEGER,
summary TEXT
);

#### Reading List Table
SQL
CREATE TABLE reading_list (
id INTEGER PRIMARY KEY AUTOINCREMENT,
user_id INTEGER NOT NULL,
book_id VARCHAR(20) NOT NULL,
status VARCHAR(20),
progress INTEGER DEFAULT 0,
started_at DATETIME,
finished_at DATETIME,
FOREIGN KEY (user_id) REFERENCES user(id),
FOREIGN KEY (book_id) REFERENCES book(id)
);


### Data Technologies
- **Database**: SQLite3
    - Chosen for its simplicity and portability
    - No separate server required
    - Perfect for medium-sized applications

- **ORM**: SQLAlchemy
    - Provides object-relational mapping
    - Simplifies database operations
    - Supports migration management

- **External Data**: Google Books API
    - RESTful API integration
    - JSON data format
    - Cached responses for performance


