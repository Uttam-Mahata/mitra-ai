# Data Models

The backend uses Pydantic models for data validation, serialization, and documentation. These models define the structure of the data used throughout the application.

## Chat Models (`chat.py`)

These models are used for handling chat-related data.

- **`MessageRole`**: An `Enum` representing the role of the message sender (`USER`, `ASSISTANT`, `SYSTEM`).
- **`MessageType`**: An `Enum` for the type of message (`TEXT`, `AUDIO`, `IMAGE`, `STRUCTURED`).
- **`ChatMode`**: An `Enum` for the chat interaction mode (`TEXT`, `VOICE`, `MULTIMODAL`).
- **`SafetyStatus`**: An `Enum` for the safety assessment status of a message (`SAFE`, `WARNING`, `CRISIS`).
- **`MessageContent`**: A `BaseModel` for the content of a message, which can include text, audio, image, or structured data.
- **`ChatMessage`**: A `BaseModel` representing a single chat message, including its content, role, timestamp, and safety status.
- **`ChatSession`**: A `BaseModel` for a chat session, containing a list of messages, session metadata, and other relevant information.
- **`TextChatRequest`**: The request model for sending a text message.
- **`VoiceChatRequest`**: The request model for sending a voice message.
- **`ChatResponse`**: The response model for a chat interaction.
- **`MultimodalChatRequest`**: The request model for a multimodal (text + image) chat message.
- **`SessionSummaryRequest`**: The request model for getting a session summary.
- **`SessionSummaryResponse`**: The response model for a session summary.
- **`CrisisResponse`**: The response model when a crisis is detected.

## Common Models (`common.py`)

These models are used for common API responses and data structures.

- **`APIStatus`**: An `Enum` for the status of an API response (`SUCCESS`, `ERROR`, `WARNING`).
- **`ErrorType`**: An `Enum` for the type of error that occurred.
- **`APIResponse`**: A base model for all API responses.
- **`ErrorResponse`**: A model for error responses.
- **`PaginationParams`**: A model for pagination parameters.
- **`PaginatedResponse`**: A model for paginated responses.
- **`HealthCheck`**: The response model for a health check.
- **`GroundingSource`**: A model for grounding source information.
- **`GenerationConfig`**: A model for AI generation configuration.

## User Models (`user.py`)

These models are used for user-related data.

- **`UserProvider`**: An `Enum` for the authentication provider (`ANONYMOUS`, `GOOGLE`, `APPLE`, `EMAIL`).
- **`UserStatus`**: An `Enum` for the user account status (`ACTIVE`, `INACTIVE`, `SUSPENDED`).
- **`AgeGroup`**: An `Enum` for user age groups.
- **`Gender`**: An `Enum` for gender options.
- **`VoiceOption`**: An `Enum` for available voice options.
- **`ProblemCategory`**: An `Enum` for problem categories for targeted support.
- **`UserPreferences`**: A `BaseModel` for user preferences and settings.
- **`UserProfile`**: A `BaseModel` for user profile information.
- **`CreateUserRequest`**: The request model for creating a user.
- **`OnboardingRequest`**: The request model for user onboarding.
- **`UpdateUserRequest`**: The request model for updating a user profile.
- **`LinkAccountRequest`**: The request model for linking an anonymous account.
- **`UserResponse`**: The response model for user data.

## Wellness Models (`wellness.py`)

These models are used for wellness-related features.

- **`MoodLevel`**: An `Enum` for mood levels (1-10).
- **`EmotionTag`**: An `Enum` for common emotion tags.
- **`MeditationType`**: An `Enum` for types of meditation.
- **`JournalType`**: An `Enum` for types of journal entries.
- **`ResourceType`**: An `Enum` for types of wellness resources.
- **`GeneratedResource`**: A `BaseModel` for a generated wellness resource.
- **`MoodEntry`**: A `BaseModel` for a daily mood entry.
- **`JournalEntry`**: A `BaseModel` for a journal entry.
- **`MeditationSession`**: A `BaseModel` for a meditation session record.
- **`WellnessGoal`**: A `BaseModel` for a wellness goal.
- **`CreateMoodEntryRequest`**: The request model for creating a mood entry.
- **`UpdateMoodEntryRequest`**: The request model for updating a mood entry.
- **`MoodAnalysis`**: The response model for mood pattern analysis.
- **`CreateJournalEntryRequest`**: The request model for creating a journal entry.
- **`UpdateJournalEntryRequest`**: The request model for updating a journal entry.
- **`StartMeditationRequest`**: The request model for starting a meditation session.
- **`CompleteMeditationRequest`**: The request model for completing a meditation session.
- **`GenerateMeditationRequest`**: The request model for generating a custom meditation.
- **`MeditationResponse`**: The response model for a generated meditation.
- **`WellnessInsight`**: A `BaseModel` for an individual wellness insight.
- **`WellnessDashboard`**: The response model for the wellness dashboard.
- **`WellnessInsightRequest`**: The request model for wellness insights.
- **`WellnessInsightResponse`**: The response model for wellness insights.
- **`VoiceSessionState`**: An `Enum` for voice session states.
- **`VoiceSessionRequest`**: The request model for starting a voice session.
- **`VoiceSessionResponse`**: The response model for voice session creation.
- **`VoiceSession`**: The data model for a voice session.
- **`VoiceTranscriptEvent`**: A model for a voice transcript event.
- **`VoiceInterruptionEvent`**: A model for a voice interruption event.
