# Backend Architecture

The Mitra AI backend is a robust and scalable server built with Python and FastAPI. It leverages Google's Gemini AI for its powerful conversational capabilities and Firebase for secure authentication and data storage.

## Core Technologies

- **FastAPI**: A modern, fast (high-performance) web framework for building APIs with Python 3.7+ based on standard Python type hints.
- **Gemini AI**: Google's latest generation of large language models, used for text and voice conversations, as well as other AI-powered features.
- **Firebase**: A platform developed by Google for creating mobile and web applications. It provides authentication, a NoSQL database (Firestore), and other services.
- **Pydantic**: A data validation and settings management library using Python type annotations. Pydantic enforces type hints at runtime, and provides user-friendly errors when data is invalid.

## Directory Structure

The backend code is organized into the following directories:

```
server/
├── main.py                 # FastAPI application entry point
├── core/                   # Configuration and settings
├── models/                 # Pydantic data models
├── services/               # Business logic services
├── repository/             # Data access layer
└── routers/                # API route handlers
```

### `main.py`

This is the entry point of the FastAPI application. It initializes the FastAPI app, includes the API routers, and sets up middleware.

### `core/`

This directory contains the core configuration and settings for the application. This includes:

- **`config.py`**: Loads environment variables and provides a centralized configuration object.

### `models/`

This directory contains the Pydantic data models that define the structure of the data used in the application. These models are used for request and response validation, as well as for interacting with the database.

### `services/`

This directory contains the business logic of the application. Each service is responsible for a specific domain, such as:

- **`gemini_service.py`**: Interacting with the Gemini AI API.
- **`firebase_service.py`**: Handling Firebase authentication and Firestore database operations.
- **`safety_service.py`**: Implementing crisis detection and safety features.

### `repository/`

This directory contains the data access layer of the application. The repositories are responsible for all interactions with the database. This separation of concerns makes the code more modular and easier to test.

- **`firestore_repository.py`**: Implements the repository pattern for interacting with Firestore.

### `routers/`

This directory contains the API route handlers. Each router corresponds to a specific set of API endpoints, such as:

- **`chat.py`**: Handles all chat-related endpoints.
- **`wellness.py`**: Manages wellness-related features like mood tracking and journaling.
- **`user.py`**: Responsible for user management and authentication.
