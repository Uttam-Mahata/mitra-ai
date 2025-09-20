# Services

The backend logic is encapsulated in a set of services, each with a specific responsibility. This modular approach enhances maintainability and testability.

## Gemini AI Services

The services responsible for interacting with the Google Gemini AI are structured in a modular and composite way.

### `BaseGeminiService`

This service provides the core functionality for all other Gemini-based services. It handles:

- Initialization of the Gemini client.
- Setting the system instructions for Mitra AI.
- Common utility methods.

### `TextGenerationService`

This service is responsible for all text generation and structured content creation. Its capabilities include:

- Generating text responses based on conversation history.
- Creating structured content using JSON schemas.
- Integrating with Google Search for grounding.

### `VoiceService`

This service handles all voice-related processing:

- Converting voice input to text (speech-to-text).
- Generating voice responses from text (text-to-speech).
- Integrating with the Live API for real-time voice conversations.

### `ImageService`

This service is dedicated to image generation and editing:

- Creating images from text prompts.
- Editing existing images based on text instructions.

### `WellnessService`

This service provides AI-powered wellness features:

- Generating custom meditation scripts.
- Creating wellness insights from user data.
- Generating personalized coping strategies.

### `GeminiService` (Composite)

This service acts as a facade, providing a single entry point to all the specialized Gemini services. It maintains backward compatibility and delegates calls to the appropriate service.

## Other Services

### `FirebaseService`

This service is responsible for all interactions with Firebase. It handles:

- **Firebase Authentication:** User creation, verification, and management.
- **Firestore:** All database operations, including creating, reading, updating, and deleting documents for users, chat sessions, mood entries, etc.
- **Firebase Storage:** Uploading, downloading, and managing files, such as user profile images.

### `SafetyService`

This service is crucial for ensuring user safety. It provides:

- **Crisis Detection:** Using keyword matching and pattern recognition to identify users in crisis.
- **Safety Assessment:** Analyzing conversation content to assess the risk level.
- **Crisis Intervention:** Providing immediate crisis response with helpline information and de-escalation techniques.
- **Logging:** Anonymously logging safety-related incidents for monitoring and improvement.

### `EnhancedWellnessService`

This service builds upon the basic `WellnessService` to provide more advanced and personalized wellness features. It is responsible for:

- Generating in-depth wellness insights.
- Creating comprehensive wellness plans.
- Integrating with external health data sources.

### `MCPIntegrationService`

This service handles the integration with the "Mental Health Care Provider" (MCP) system. Its main responsibilities are:

- Generating tech-aware resources for chat sessions.
- Facilitating the connection between users and human therapists.
- Managing the referral and appointment scheduling process.

### `ResourceGenerationService`

This service is dedicated to generating various types of resources for users, such as:

- Articles and blog posts.
- Worksheets and exercises.
- Educational content on mental health topics.

These services work together to provide a comprehensive and robust backend for the Mitra AI application.
