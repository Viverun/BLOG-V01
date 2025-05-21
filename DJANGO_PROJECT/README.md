# Django Project: AI-Assisted Blog Platform

## Overview

This project is a feature-rich blog platform built with Django and Python. It incorporates user authentication, profile management, blog post creation and management, a commenting system, tagging functionality, and integrates AI-assisted features for profile suggestions and a dedicated AI tools dashboard.

Key Technologies:
*   Python
*   Django
*   HTML
*   CSS
*   JavaScript
*   SQLite (default, can be configured for other databases)

## Project Structure

The project is organized into a main project directory and several apps:

*   `DJANGO_PROJECT/`: The root directory of the Django project.
    *   `DJANGO_PROJECT/settings.py`: Contains the main settings for the Django project, including database configuration, installed apps, middleware, static file handling, email settings, and configurations for third-party applications.
    *   `DJANGO_PROJECT/urls.py`: Defines the main URL routing for the project, including routes for the admin interface, authentication, user profiles, and the blog application.
*   `blog/`: This app handles all functionalities related to blog posts.
    *   `blog/models.py`: Defines the data models for `Tag`, `Post`, and `Comment`.
    *   `blog/views.py`: Contains the views for listing, creating, viewing, updating, and deleting blog posts, managing comments, and the AI tools dashboard.
    *   Manages blog posts, comments, tags, and related views.
*   `users/`: This app is responsible for user management.
    *   `users/models.py`: Defines the data model for user `Profile` information.
    *   `users/views.py`: Contains the views for user registration, profile viewing and editing, and AI-assisted profile suggestions.
    *   Manages user registration, profiles, authentication, and AI-assisted profile suggestions.
*   `mcp_server/`: The purpose and specific functionalities of the `mcp_server` app are not detailed in the provided information. It is present in the project structure.

## Key Features

*   **User Management:**
    *   User registration with email verification (if configured).
    *   Login and logout functionality.
    *   Password reset mechanism.
    *   User profiles with customizable bios and profile image uploads.
*   **Blogging:**
    *   Create, Read, Update, and Delete (CRUD) operations for blog posts.
    *   Summernote WYSIWYG editor for rich text formatting in blog posts.
    *   Commenting system with support for threaded replies.
    *   Tagging system to categorize blog posts.
    *   Display of popular tags.
*   **AI-Assisted Features:**
    *   AI-assisted profile suggestions (via the `profile_ai_assist` view in the `users` app) to help users populate their profiles.
    *   AI tools dashboard (via the `blog_ai_tools_dashboard` view in the `blog` app) providing access to various AI-powered utilities.
*   **Other:**
    *   Display of a random quote or joke on the homepage for user engagement.

## Setup and Running the Project

1.  **Clone the Repository:**
    ```bash
    git clone <repository-url>
    cd DJANGO_PROJECT
    ```

2.  **Install Dependencies:**
    Dependencies are listed in `pyproject.toml`. It's recommended to use a virtual environment.
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`
    pip install -r requirements.txt # Assuming a requirements.txt is generated from pyproject.toml or poetry
    # If using poetry:
    # pip install poetry
    # poetry install
    ```
    *(Note: If a `requirements.txt` is not present, you might need to generate it using `poetry export -f requirements.txt --output requirements.txt --without-hashes` if Poetry is used, or manually list them if `pyproject.toml` is for another build system like Flit or Hatch.)*

3.  **Set up Environment Variables:**
    Create a `.env` file in the `DJANGO_PROJECT` root directory and add the following variables. For development, you can often rely on default settings in `settings.py` if they are configured for development mode.
    ```env
    DJANGO_SECRET_KEY='your_secret_key_here'
    DJANGO_DEBUG=True
    # Email settings (if not using console backend for development)
    # EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
    # EMAIL_HOST = 'smtp.example.com'
    # EMAIL_PORT = 587
    # EMAIL_USE_TLS = True
    # EMAIL_HOST_USER = 'your_email@example.com'
    # EMAIL_HOST_PASSWORD = 'your_email_password'
    ```
    *(Ensure `settings.py` is configured to read these, e.g., using `python-decouple` or `os.getenv`)*

4.  **Set up the Database:**
    Apply database migrations to create the necessary tables.
    ```bash
    python manage.py migrate
    ```

5.  **Create a Superuser (Optional but Recommended):**
    This allows access to the Django admin interface.
    ```bash
    python manage.py createsuperuser
    ```

6.  **Run the Development Server:**
    ```bash
    python manage.py runserver
    ```
    The application will typically be available at `http://127.0.0.1:8000/`.

## File Details

*   `DJANGO_PROJECT/README.md`: This file, providing an overview of the project.
*   `DJANGO_PROJECT/DJANGO_PROJECT/settings.py`: Main Django project settings. This file configures the database, installed applications (like `blog` and `users`), middleware, template directories, static file handling, email backend, and any third-party application settings (e.g., `crispy_forms`, `allauth`, `summernote`).
*   `DJANGO_PROJECT/DJANGO_PROJECT/urls.py`: Main URL routing file for the project. It includes URL patterns for the Django admin site, authentication views (login, logout, password reset provided by `django.contrib.auth.urls` or a third-party app like `allauth`), user profile URLs, and includes the URL configurations from the `blog` app (e.g., `path('blog/', include('blog.urls'))`).
*   `DJANGO_PROJECT/blog/models.py`: Defines the database schema for the `blog` application.
    *   `Tag`: Model for blog post tags.
    *   `Post`: Model for blog posts, likely including fields for title, content, author (ForeignKey to User), publication date, tags (ManyToManyField to `Tag`), etc.
    *   `Comment`: Model for comments on blog posts, likely with a ForeignKey to `Post` and `User`, and possibly a self-referential ForeignKey for threaded comments.
*   `DJANGO_PROJECT/users/models.py`: Defines the database schema for the `users` application.
    *   `Profile`: Extends the default Django `User` model (often via a OneToOneField) to include additional user information like bio, profile picture, etc.
*   `DJANGO_PROJECT/blog/views.py`: Contains the Python functions or classes that handle requests and generate responses for the `blog` app. This includes views for:
    *   Displaying lists of posts (e.g., homepage, all posts, posts by tag).
    *   Displaying a single post detail.
    *   Creating, updating, and deleting posts (CRUD operations).
    *   Handling comment submission and display.
    *   The `blog_ai_tools_dashboard` view, providing access to AI-related tools for blogging.
*   `DJANGO_PROJECT/users/views.py`: Contains the Python functions or classes for user-related actions in the `users` app. This includes views for:
    *   User registration.
    *   Displaying and editing user profiles.
    *   The `profile_ai_assist` view, which uses AI to help users generate or improve their profile information.
