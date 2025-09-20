# Security Considerations

Security is a top priority for the Mitra AI backend. We have implemented several measures to protect user data and ensure the integrity of our systems.

## Authentication

- **Firebase Authentication:** We use Firebase Authentication to manage user identities. All API requests must be authenticated with a valid Firebase ID token, which is passed in the `Authorization` header as a Bearer token.
- **Token Validation:** On the backend, we use the Firebase Admin SDK to verify the ID token for every request that requires authentication. This ensures that only valid, authenticated users can access protected endpoints.
- **Anonymous Authentication:** We provide an anonymous authentication option for users who want to try the app without creating a full account. This allows us to maintain user-specific data without collecting any personal information.

## Data Privacy

- **Data Isolation:** All user data is stored in Firestore and is isolated by user ID. The application logic and Firestore security rules ensure that users can only access their own data.
- **Encryption:**
    - **In Transit:** All data transmitted between the client, backend, and external services is encrypted using TLS/SSL.
    - **At Rest:** All data stored in Firestore is encrypted at rest by Google Cloud.
- **Data Minimization:** We only collect the data that is necessary to provide our services. We do not collect any personally identifiable information (PII) unless the user voluntarily provides it (e.g., by creating a permanent account with an email address).
- **User Control:** Users have the ability to delete their own data at any time.

## Input Validation

- **Pydantic Models:** We use Pydantic models to define the expected structure and types of all incoming request data. FastAPI automatically validates incoming requests against these models, which helps prevent common vulnerabilities like injection attacks and data corruption.

## Rate Limiting

- **Abuse Prevention:** We recommend configuring rate limiting on our production environment to prevent abuse and ensure fair usage of our services. This can be done using a service like Google Cloud Armor.

## CORS (Cross-Origin Resource Sharing)

- **Restricted Access:** We have configured CORS to only allow requests from authorized client domains. This prevents other websites from making requests to our API on behalf of a user.

## Crisis Logging

- **Anonymous Logging:** When our `SafetyService` detects a potential crisis situation, it logs the incident for monitoring and analysis. This logging is done anonymously to protect user privacy. We do not store the content of the crisis messages, only anonymized metadata about the incident.

## Secure Development Practices

- **Dependency Scanning:** We regularly scan our dependencies for known vulnerabilities and update them as needed.
- **Code Reviews:** All code changes are reviewed by another developer before being merged into the main branch.
- **Principle of Least Privilege:** Our service accounts and IAM roles are configured with the minimum permissions necessary to perform their functions.
