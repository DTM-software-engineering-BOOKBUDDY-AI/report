
---
title: Design
has_children: false
nav_order: 4
---
# BookBuddy Design Documentation

================================

Design Planning Phase
---------------------

We began our design process by creating detailed mockups in Figma, which helped us visualize and plan the entire website structure. The main pages we designed were:

*   Homepage

*   Login Page

*   Sign Up Page

*   User Profile Page

*   My Library Page

*   Recommendation Page

*   Form Page for User Preferences

here is the link for the initial figma design: https://www.figma.com/design/Bc71oSWs5TwCr5pAoqPPGJ/Book-Store-UI%2FUX-(Community)?node-id=0-1&m=dev&t=psbOBtij8NlGUzTT-1

Implementation Approach
-----------------------

### 1\. Initial HTML & CSS Development

We started by building the basic structure of each page using HTML and CSS. Our focus was on creating a clean and user-friendly interface. The initial CSS implementation included:

*   A consistent color scheme

*   Basic layout structures



### 2\. Bootstrap Enhancement

To improve the website's appearance and responsiveness, we integrated Bootstrap framework. This helped us with:

*   Creating responsive layouts that work well on all devices

*   Adding pre-styled components like buttons and forms

*   Implementing a grid system for better content organization

*   Ensuring consistent spacing and alignment


### 3\. Page-Specific Design Features

#### Homepage

*   Welcoming hero section with engaging visuals

*   Featured books section

*   Clear navigation menu

*   Call-to-action buttons for sign-up and recommendations


#### Authentication Pages (Login/Signup)

*   Clean, centered forms

*   Clear input fields

*   Validation feedback

*   User-friendly error messages


#### My Library

*   Grid layout for book display

*   Book cards with hover effects

*   Reading progress indicators

*   Easy-to-use sorting and filtering options


#### Recommendation Page

*   Interactive preference form

*   Visual feedback for selections

*   Clear submission process

*   Attractive book suggestion display


#### Profile Page

*   User information display

*   Edit functionality

*   Reading statistics

*   Preference management


### 4\. Responsive Design

We ensured the website works well on all devices by:

*   Using flexible layouts

*   Implementing responsive images

*   Adjusting text sizes for different screens

*   Creating mobile-friendly navigation


### 5\. Visual Enhancements

To make the website more engaging, we added:

*   Smooth transitions between pages

*   Hover effects on interactive elements

*   Loading animations

*   Consistent button styles

*   Clear visual feedback for user actions


This design process helped us create a cohesive and user-friendly website that not only looks good but also provides a smooth and intuitive user experience. The combination of careful planning in Figma and implementation using HTML, CSS, and Bootstrap resulted in a modern and functional book recommendation platform.

BookBuddy Recommendation System Documentation
=============================================

Overview
--------

The BookBuddy recommendation system uses a hybrid approach combining content-based filtering and natural language processing to match books with user preferences. The system operates in several stages: preference processing, book search, and similarity matching.

1\. User Preference Processing
------------------------------

### Data Collection

The system collects user preferences across multiple dimensions:

*   Genres

*   Themes

*   Mood

*   Language

*   Length preferences

*   Maturity level

*   Reading style


### Preference Text Generation
\# Example of preference text format:

(`genres:fantasy theme:adventure mood:exciting style:series maturity:young`)
2\. Book Search Process
-----------------------

### Query Generation

The system converts user preferences into natural language search queries using templates:

templates = \[
"{genre} books with {theme} themes",
"{mood} {genre} novels",
"{genre} {style} for {maturity} readers"
\# ... more templates
\]
### API Integration

*   Uses Google Books API for book retrieval

*   Applies language restrictions (English)

*   Sets relevance-based ordering

*   Fetches up to 40 results per query


3\. Book Filtering
------------------

### Essential Information Check

Books must have:

*   Title

*   Authors

*   Description


### Category Filtering

#### Required Categories (at least one):

*   Fiction

*   Adventure

*   Action and adventure

*   Juvenile fiction


#### Excluded Categories:

*   Non-fiction

*   Education

*   Textbook

*   Manual

*   Guide

*   Science

*   Copyright


### Content Verification

Description must contain adventure-related terms:

*   Adventure

*   Quest

*   Journey

*   Expedition

*   Explore

*   Discovery


4\. Similarity Calculation
--------------------------

### Text Processing

*   Converts both user preferences and book information into weighted feature texts

*   Uses TF-IDF (Term Frequency-Inverse Document Frequency) vectorization

*   Removes English stop words


### Feature Weighting

Books are represented by features including:

*   Categories (genres)

*   Description

*   Language

*   Page count (length category)

*   Maturity rating

*   Authors


### Similarity Score

*   Uses cosine similarity between user preference vector and book feature vector

*   Scores range from 0 (no similarity) to 1 (perfect match)

*   Formula: \\\[ similarity = \\cos(\\theta) = \\frac{A \\cdot B}{||A|| ||B||} \\\]


5\. Recommendation Generation
-----------------------------

1\. Calculates similarity scores for all filtered books

*   Sorts books by similarity score in descending order


3\. Returns top N recommendations (default: 5)

*   Includes detailed book information and similarity scores


Example Output
--------------
Top 5 Book Recommendations:

\--------------------------------------------------

1\. \[Book Title\]

Authors: \[Author Names\]

Similarity Score: 0.85

Categories: Fantasy, Adventure

Language: English

Rating: 4.5/5

Description: \[First 150 characters...\]

Debug Features
--------------

The system includes debugging capabilities to:

*   View raw user preference text

*   Examine book feature text

*   Analyze similarity calculations

*   Track query generation

*   Monitor API responses


This recommendation system prioritizes finding books that closely match user preferences while ensuring content quality and relevance through multiple layers of filtering and matching.
