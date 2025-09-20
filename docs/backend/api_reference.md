# API Reference

This document provides a detailed reference for the Mitra AI backend API.

## Authentication

All API endpoints require a valid Firebase ID token to be passed in the `Authorization` header.

**Header Format:**

```
Authorization: Bearer <firebase_id_token>
```

## API Base Path

All API endpoints are prefixed with `/api/v1`.

---

## Chat API

**Base Path:** `/api/v1/chat`

Handles all chat-related functionalities, including text, voice, and multimodal conversations.

### `POST /text`

Send a text message to Mitra.

- **Request Body:** `TextChatRequest`
- **Response Body:** `ChatResponse`

**`TextChatRequest` Model:**

| Field | Type | Description |
|---|---|---|
| `message` | `str` | The text message from the user. |
| `session_id` | `Optional[str]` | The ID of the chat session. If not provided, a new session will be created. |
| `problem_category`| `Optional[ProblemCategory]` | The problem category for the chat session. |
| `include_grounding`| `Optional[bool]` | Whether to include grounding sources in the response. |
| `generate_image`| `Optional[bool]` | Whether to generate an image based on the message. |

### `POST /voice`

Send a voice message to Mitra.

- **Request Body:** `multipart/form-data` with `audio_file`
- **Response Body:** `ChatResponse`

**Form Data:**

| Field | Type | Description |
|---|---|---|
| `audio_file` | `UploadFile` | The audio file of the user's voice message. |
| `session_id` | `Optional[str]` | The ID of the chat session. If not provided, a new session will be created. |
| `response_format`| `Optional[str]` | The desired response format (`audio` or `text`). |

### `POST /multimodal`

Send a multimodal message (text + image) to Mitra.

- **Request Body:** `MultimodalChatRequest`
- **Response Body:** `ChatResponse`

**`MultimodalChatRequest` Model:**

| Field | Type | Description |
|---|---|---|
| `text` | `Optional[str]` | The text part of the message. |
| `image_data` | `Optional[bytes]` | The image data as a base64 encoded string. |
| `session_id` | `Optional[str]` | The ID of the chat session. If not provided, a new session will be created. |
| `operation` | `str` | The operation to perform (`describe`, `generate`, `edit`). |

### `GET /session/{session_id}`

Get a summary of a chat session.

- **Path Parameter:** `session_id` (str)
- **Response Body:** `SessionSummaryResponse`

### `GET /sessions`

Get a list of the user's chat sessions.

- **Response Body:** `List[SessionSummaryResponse]`

### `DELETE /session/{session_id}`

Delete a chat session.

- **Path Parameter:** `session_id` (str)
- **Response Body:** `{"message": "Session deleted successfully"}`

---

## Wellness API

**Base Path:** `/api/v1/wellness`

Manages wellness features like mood tracking, journaling, and meditation.

### `POST /mood`

Create a new mood entry.

- **Request Body:** `CreateMoodEntryRequest`
- **Response Body:** `MoodEntry`

### `GET /mood`

Get mood entries for the current user.

- **Query Parameters:** `limit` (int), `start_date` (date), `end_date` (date)
- **Response Body:** `List[MoodEntry]`

### `PUT /mood/{entry_id}`

Update an existing mood entry.

- **Path Parameter:** `entry_id` (str)
- **Request Body:** `UpdateMoodEntryRequest`
- **Response Body:** `MoodEntry`

### `GET /mood/analysis`

Get mood pattern analysis and insights.

- **Query Parameters:** `days` (int)
- **Response Body:** `MoodAnalysis`

### `POST /journal`

Create a new journal entry.

- **Request Body:** `CreateJournalEntryRequest`
- **Response Body:** `JournalEntry`

### `GET /journal`

Get journal entries for the current user.

- **Query Parameters:** `limit` (int)
- **Response Body:** `List[JournalEntry]`

### `PUT /journal/{entry_id}`

Update an existing journal entry.

- **Path Parameter:** `entry_id` (str)
- **Request Body:** `UpdateJournalEntryRequest`
- **Response Body:** `JournalEntry`

### `POST /journal/guided-prompt`

Get a guided journaling prompt.

- **Response Body:** `{"prompt": "..."}`

### `POST /meditation/generate`

Generate a custom meditation session.

- **Request Body:** `GenerateMeditationRequest`
- **Response Body:** `MeditationResponse`

### `POST /meditation/{session_id}/complete`

Mark a meditation session as completed.

- **Path Parameter:** `session_id` (str)
- **Response Body:** `{"message": "Meditation session completed successfully"}`

### `GET /dashboard`

Get the user's wellness dashboard.

- **Response Body:** `WellnessDashboard`

---

## User API

**Base Path:** `/api/v1/user`

Handles user authentication, profile management, and preferences.

### `POST /create-anonymous`

Create an anonymous user account.

- **Response Body:** `UserResponse`

### `GET /profile`

Get the current user's profile.

- **Response Body:** `UserResponse`

### `PUT /profile`

Update the user's profile.

- **Request Body:** `UpdateUserRequest`
- **Response Body:** `UserResponse`

### `POST /link-account`

Link an anonymous account to a permanent account.

- **Request Body:** `LinkAccountRequest`
- **Response Body:** `UserResponse`

### `POST /signin`

Sign in an existing user.

- **Request Body:** `{"id_token": "..."}`
- **Response Body:** `{"message": "Sign in successful", "user_id": "..."}`

### `POST /refresh-session`

Refresh the user's session.

- **Response Body:** `{"message": "Session refreshed"}`

### `DELETE /account`

Delete the user's account.

- **Response Body:** `{"message": "Account deletion initiated"}`

### `GET /preferences`

Get the user's preferences.

- **Response Body:** `UserPreferences`

### `PUT /preferences`

Update the user's preferences.

- **Request Body:** `UserPreferences`
- **Response Body:** `UserPreferences`

### `GET /stats`

Get user activity statistics.

- **Response Body:** `dict`
