---
title: Design
has_children: false
nav_order: 4
---

# Design
# Bookbuddy Design Document

This document contains the UML diagrams that describe the architecture and behavior of the Bookbuddy application, following the C4 model for visualizing software architecture.

---

## Level 1: System Context Diagram

This diagram provides a high-level overview of the system, showing how it interacts with its users and other systems.

```mermaid
useCaseDiagram
    actor "Guest" as Guest
    actor "Registered User" as User

    User --|> Guest

    rectangle "Bookbuddy System" {
        usecase "Search for Books" as UC1
        usecase "View Book Details" as UC2
        usecase "Register Account" as UC3
        usecase "Log In" as UC4
        usecase "Manage Profile" as UC5
        usecase "Manage Reading List" as UC6
        usecase "Get Book Recommendations" as UC7
        usecase "Log Out" as UC8
    }

    Guest -- (UC1)
    Guest -- (UC2)
    Guest -- (UC3)
    Guest -- (UC4)

    User -- (UC5)
    User -- (UC6)
    User -- (UC7)
    User -- (UC8)
```

---

## Level 2: Container Diagram

This diagram zooms into the system to show the high-level containers (applications, data stores, etc.) and their interactions.

```mermaid
deploymentDiagram
    node "User's Computer/Mobile" {
        artifact "Web Browser" as Browser
    }

    node "Cloud Platform (e.g., Vercel)" {
        node "Application Server" {
            artifact "Bookbuddy Flask App" as App
        }
        node "Database Server" {
            artifact "Bookbuddy DB" as DB
        }
    }

    node "Google's Infrastructure" {
        artifact "Google Books API" as GoogleAPI
    }

    Browser ->> App : HTTPS
    App ->> DB : DB Connection
    App ->> GoogleAPI : API Requests (HTTPS)
```

---

## Level 3: Component & Package Diagrams

These diagrams zoom into a container to show the components and packages within it.

### Component Diagram

This diagram illustrates the major components of the Bookbuddy application and their dependencies.

```mermaid
componentDiagram
    actor User

    node "Client Device" {
        [Web Browser] as Browser
    }

    node "Web Server (e.g., Vercel)" {
        package "Flask Application" {
            [Routes]
            [Forms]
            [Models]
            [Services]
        }
        [Database (SQLite)]
    }

    node "Google Cloud" {
        [Google Books API]
    }

    User -->> Browser
    Browser -->> Routes : HTTP Requests
    Routes -->> Forms : Validation
    Routes -->> Services : Business Logic
    Routes -->> Models : Data Access
    Services -->> Models
    Services -->> [Google Books API] : External API Calls
    Models -->> [Database (SQLite)] : CRUD Operations
```

### Package Diagram

This diagram shows the structure of the codebase in terms of packages (namespaces or folders).

```mermaid
packageDiagram
    package "Bookbuddy" {
        package "routes" {
            [books.py]
        }
        package "services" {
            [google_books.py]
            [cache_service.py]
        }
        package "templates" {}
        [app.py]
        [models.py]
        [forms.py]
        [config.py]
        [extensions.py]
        [Recommendation.py]
    }

    [app.py] --> [routes.books.py]
    [app.py] --> [models.py]
    [app.py] --> [forms.py]
    [app.py] --> [Recommendation.py]
    [routes.books.py] --> [services.google_books.py]
    [services.google_books.py] --> [services.cache_service.py]
    [Recommendation.py] --> [models.py]
```

---

## Level 4: Code (Class Diagrams)

This diagram zooms into a component to show the implementation details.

```mermaid
classDiagram
    class User {
        +Integer id
        +String email
        +String username
        +String password_hash
        +DateTime created_at
        +String profile_picture
        +Text bio
        +String gender
        +String birthday
        +String telephone
        +String language
        +String privacy
        +Text friends_list
        +Text block_list
        +Text hide_list
        +set_password(password)
        +check_password(password)
    }

    class UserPreferences {
        +Integer id
        +Integer user_id
        +String style
        +String theme
        +String mood
        +String length
        +String pace
        +String language
        +String maturity
        +String genres
        +Integer reading_goal
        +Boolean email_notifications
    }

    class ReadingList {
        +Integer id
        +Integer user_id
        +Integer book_id
        +String status
        +Integer progress
        +DateTime started_at
        +DateTime finished_at
    }

    class Book {
        +Integer id
        +String title
        +String author
        +String cover_image
        +String genre
        +String language
        +Integer publication_year
        +Text summary
    }

    class BookRecommender {
        +UserPreferences preferences
        +TfidfVectorizer vectorizer
        +get_weighted_text(text, weight, feature_name)
        +get_user_preference_text(user_id)
        +get_book_text(book_data)
        +calculate_similarity(user_id, book_data)
        +get_recommendations(user_id, book_list, num_recommendations)
        +debug_similarity(user_id, book_data)
        +process_google_books_response(books)
    }

    class GoogleBooksAPI {
        +String BASE_URL
        +String api_key
        +search_books(query, max_results)
        +get_book_details(book_id)
        +_parse_books(items)
        +_parse_book_details(data)
    }

    class CacheService {
        +String cache_dir
        +Integer expiry_hours
        +get(key)
        +set(key, value)
    }

    class SignupForm {
        +StringField username
        +EmailField email
        +PasswordField password
        +PasswordField confirm_password
        +SelectField gender
        +DateField birthday
        +SubmitField submit
        +validate_username(username)
        +validate_email(email)
        +validate_birthday(birthday)
    }

    class LoginForm {
        +EmailField email
        +PasswordField password
        +SubmitField submit
    }

    class ProfileForm {
        +StringField username
        +SelectField gender
        +TextAreaField bio
        +StringField birthday
        +StringField telephone
        +StringField language
        +SelectField privacy
        +StringField friends_list
        +StringField block_list
        +StringField hide_list
        +validate_username(username)
        +validate_bio(field)
    }

    User "1" -- "1" UserPreferences : has
    User "1" -- "0..*" ReadingList : has
    Book "1" -- "0..*" ReadingList : contains
    BookRecommender -- UserPreferences : uses
    GoogleBooksAPI -- CacheService : uses
    
    Flask_App -- User
    Flask_App -- Book
    Flask_App -- ReadingList
    Flask_App -- UserPreferences
    
    class Flask_App {
        +create_app()
    }

    User --|> db.Model
    UserMixin --|> User
    UserPreferences --|> db.Model
    ReadingList --|> db.Model
    Book --|> db.Model
    
    SignupForm --|> FlaskForm
    LoginForm --|> FlaskForm
    ProfileForm --|> FlaskForm
```

---

## Behavioral Diagrams

These diagrams describe the behavior of the system.

### Sequence Diagrams

Sequence diagrams illustrate how objects interact with each other over time. These diagrams show the sequence of messages exchanged between objects to perform a specific task.

#### User Signup
```mermaid
sequenceDiagram
    participant User
    participant Browser
    participant Flask_App
    participant Database

    User->>Browser: Fills and submits signup form
    Browser->>Flask_App: POST /signup
    Flask_App->>Flask_App: Validates form data
    alt Form is valid
        Flask_App->>Database: Creates User and UserPreferences records
        Database-->>Flask_App: Confirms creation
        Flask_App->>Browser: Redirects to /login
        Browser->>User: Shows login page with success message
    else Form is invalid
        Flask_App->>Browser: Renders signup page with errors
        Browser->>User: Shows signup page with error messages
    end
```

#### User Login
```mermaid
sequenceDiagram
    participant User
    participant Browser
    participant Flask_App
    participant Database

    User->>Browser: Fills and submits login form
    Browser->>Flask_App: POST /login
    Flask_App->>Flask_App: Validates form data
    alt Form is valid
        Flask_App->>Database: Queries for user by email
        Database-->>Flask_App: Returns user data
        Flask_App->>Flask_App: Checks password
        alt Password is correct
            Flask_App->>Flask_App: Logs in user
            Flask_App->>Browser: Redirects to /home
            Browser->>User: Shows homepage
        else Password is incorrect
            Flask_App->>Browser: Renders login page with error
            Browser->>User: Shows login page with error message
        end
    else Form is invalid
        Flask_App->>Browser: Renders login page with errors
        Browser->>User: Shows login page with error messages
    end
```

#### Book Recommendation
```mermaid
sequenceDiagram
    participant User
    participant Browser
    participant Flask_App
    participant BookRecommender
    participant GoogleBooksAPI
    participant Database

    User->>Browser: Submits recommendation form
    Browser->>Flask_App: POST /recommendation
    Flask_App->>Database: Saves UserPreferences
    Database-->>Flask_App: Confirms save
    Flask_App->>BookRecommender: Creates instance
    BookRecommender->>Database: Gets user preferences
    Database-->>BookRecommender: Returns preferences
    BookRecommender->>GoogleBooksAPI: Fetches books based on preferences
    GoogleBooksAPI-->>BookRecommender: Returns book data
    BookRecommender->>BookRecommender: Calculates recommendations
    BookRecommender-->>Flask_App: Returns recommended books
    Flask_App->>Browser: Renders recommendation page with results
    Browser->>User: Shows recommended books
```

#### Adding a Book to Reading List
```mermaid
sequenceDiagram
    participant User
    participant Browser
    participant Flask_App
    participant Database

    User->>Browser: Clicks 'Add to Reading List'
    Browser->>Flask_App: POST /add-to-reading-list (AJAX)
    Flask_App->>Database: Checks if book exists
    alt Book exists
        Database-->>Flask_App: Returns existing book
    else Book does not exist
        Flask_App->>Database: Creates new book
        Database-->>Flask_App: Confirms creation
    end
    Flask_App->>Database: Creates or updates ReadingList entry
    Database-->>Flask_App: Confirms update
    Flask_App->>Browser: Returns JSON success response
    Browser->>User: Updates UI to show book in reading list
```

### Activity Diagrams

Activity diagrams describe the flow of control in a process. They are useful for modeling the business logic and workflows of the application.

#### User Registration
```mermaid
activityDiagram
    title User Registration

    start
    :User navigates to signup page;
    :Fills in registration form;
    :Submits form;
    if (Form validation fails) then (no)
        :Show error messages;
        :User corrects information;
        stop
    else (yes)
        :Create new User object;
        :Hash password;
        :Create UserPreferences object;
        :Save User and UserPreferences to database;
        :Redirect to login page;
        :Show success message;
    endif
    stop
```

#### User Login
```mermaid
activityDiagram
    title User Login

    start
    :User navigates to login page;
    :Fills in login form;
    :Submits form;
    :Query database for user by email;
    if (User exists) then (yes)
        :Check password;
        if (Password is correct) then (yes)
            :Log in user;
            :Redirect to homepage;
        else (no)
            :Show invalid credentials error;
        endif
    else (no)
        :Show invalid credentials error;
    endif
    stop
```

#### Book Recommendation
```mermaid
activityDiagram
    title Book Recommendation

    start
    :User navigates to recommendation form;
    :Fills in preferences;
    :Submits form;
    :Save UserPreferences to database;
    :Get search queries from preferences;
    :Fetch books from Google Books API;
    :Process and clean book data;
    :Calculate similarity between user preferences and books;
    :Sort books by similarity;
    :Select top recommendations;
    :Render recommendation page with results;
    stop
```

#### Adding a Book to Reading List
```mermaid
activityDiagram
    title Adding a Book to Reading List

    start
    :User searches for a book;
    :User clicks 'Add to Reading List' button;
    :Send AJAX request to /add-to-reading-list;
    :Check if book exists in database;
    if (Book does not exist) then (yes)
        :Create new Book object;
        :Save book to database;
    endif
    :Check if ReadingList entry exists for user and book;
    if (Entry exists) then (yes)
        :Update status of existing entry;
    else (no)
        :Create new ReadingList entry;
        :Save entry to database;
    endif
    :Return JSON success response;
    :Update UI to reflect change;
    stop
```

### State Diagram

This state diagram shows the transitions between states of a `Book` object within a user's reading list.

#### Book Status in Reading List
```mermaid
stateDiagram-v2
    [*] --> Not_In_Library

    Not_In_Library --> Want_to_Read: Add to list
    Want_to_Read --> Currently_Reading: Start reading
    Currently_Reading --> Finished: Finish reading

    Want_to_Read --> Not_In_Library: Remove from list
    Currently_Reading --> Want_to_Read: Stop reading
    Finished --> Currently_Reading: Reread book
```




*   Monitor API responses


This recommendation system prioritizes finding books that closely match user preferences while ensuring content quality and relevance through multiple layers of filtering and matching.
