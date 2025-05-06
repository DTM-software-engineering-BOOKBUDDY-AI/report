---
title: Future work
has_children: false
nav_order: 13
---

# Known issues and future work

----------------------------

This section outlines the current limitations of the Bookbuddy project, including missing functionalities and aspects that do not perform as intended. It also proposes potential future developments to enhance and expand the software. We aim to be transparent about these areas, understanding they represent opportunities for growth.

### Known Issues

The following are identified areas where the software is currently lacking or not functioning optimally:

1.  **User Profile and Social Features:**

    -   **Profile Photo Update:** Users are currently unable to change their profile photo via the dashboard.
    -   **Friend System:** The functionality for users to add and interact with friends has not been implemented.
    -   **Book Notes:** Users cannot add personal notes or annotations to the books in their library.
2.  **Recommendation System:**

    -   **Accuracy for Certain Selections:** The recommendation system does not always provide perfectly aligned suggestions for all user input combinations in the discovery questionnaire.
    -   **Language Restriction:** A significant issue with the recommendation API was its tendency to default to Italian results (likely based on server location). To mitigate this, a restriction was implemented to fetch only English books. Consequently, even if a user selects a different language in the discovery form, they currently only receive English book recommendations.
3.  **Content Display:**

    -   **Book Summary Parsing:** On the book details page, the summary of the book is sometimes not parsed correctly, leading to the display of raw HTML tags instead of formatted text.

### Future Work

To address the current limitations and to further develop the Bookbuddy platform, the following enhancements and expansions are proposed:

1.  **Core Feature Implementation & Bug Fixes:**

    -   Enable users to change their profile photos.
    -   Implement the "add friends" functionality to foster a social community.
    -   Allow users to add personal notes to books in their virtual library.
    -   Refine the book summary parsing logic on the book details page to correctly display formatted text and eliminate HTML tags.
2.  **Recommendation System Enhancements:**

    -   Investigate and improve the recommendation algorithm to provide more accurate results across a wider range of user selections.
    -   Resolve the language issue in the recommendation system. This would involve modifying the API interaction to respect the user's chosen language in the discovery form, rather than defaulting to or being restricted to English.
    -   Introduce a new recommendation feature that suggests books based on the existing contents of a user's virtual library (e.g., "Because you read X, you might like Y").
3.  **Website Expansion and SEO:**

    -   Develop additional static pages such as "Contact Us," "About Us," and a "Blog" section. These pages would not only provide more information to users but also contribute positively to the website's Search Engine Optimization (SEO).
