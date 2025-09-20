# Deployment

This document provides instructions for deploying the Mitra AI backend to a production environment.

## Prerequisites

Before deploying the application, ensure you have the following:

- A Google Cloud Platform (GCP) project.
- A Firebase project linked to your GCP project.
- The `gcloud` command-line tool installed and configured.

## Production Deployment Steps

### 1. Configure Firebase Admin SDK

For the backend to communicate with Firebase services, you need to set up a service account.

1.  **Create a service account:**
    - In the GCP Console, go to **IAM & Admin > Service Accounts**.
    - Select your project and click **Create Service Account**.
    - Give the service account a name (e.g., `mitra-backend-service`).
    - Grant the service account the following roles:
        - `Firebase Admin`
        - `Cloud Datastore User`
        - `Storage Admin`
    - Click **Done**.

2.  **Generate a private key:**
    - Find the service account you just created in the list.
    - Click the three-dot menu under **Actions** and select **Manage keys**.
    - Click **Add Key > Create new key**.
    - Choose **JSON** as the key type and click **Create**.
    - A JSON file will be downloaded to your computer. Keep this file secure, as it provides administrative access to your Firebase project.

### 2. Set Up a Container Platform

We recommend using a serverless container platform like **Google Cloud Run** for deploying the backend. Cloud Run automatically scales your application up or down based on traffic, and you only pay for the resources you use.

1.  **Enable the Cloud Run API:**
    - In the GCP Console, go to **APIs & Services > Library**.
    - Search for "Cloud Run Admin API" and click **Enable**.

2.  **Create a `Dockerfile`:**
    - In the `server` directory, create a `Dockerfile` with the following content:

    ```Dockerfile
    # Use the official Python image
    FROM python:3.9-slim

    # Set the working directory
    WORKDIR /app

    # Copy the requirements file and install dependencies
    COPY requirements.txt .
    RUN pip install --no-cache-dir -r requirements.txt

    # Copy the application code
    COPY . .

    # Expose the port the app runs on
    EXPOSE 8000

    # Run the application
    CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
    ```

3.  **Build and push the container image:**
    - In your terminal, navigate to the `server` directory.
    - Run the following commands to build the container image and push it to Google Container Registry (GCR):

    ```bash
    # Set your GCP project ID
    export PROJECT_ID=[your-gcp-project-id]

    # Build the container image
    gcloud builds submit --tag gcr.io/$PROJECT_ID/mitra-backend

    # Push the image to GCR
    gcloud docker -- push gcr.io/$PROJECT_ID/mitra-backend
    ```

4.  **Deploy to Cloud Run:**
    - Run the following command to deploy the container image to Cloud Run:

    ```bash
    gcloud run deploy mitra-backend \
      --image gcr.io/$PROJECT_ID/mitra-backend \
      --platform managed \
      --region [your-gcp-region] \
      --allow-unauthenticated \
      --set-env-vars GOOGLE_API_KEY=[your-gemini-api-key],FIREBASE_PROJECT_ID=[your-firebase-project-id]
    ```

    - When prompted, confirm the deployment.
    - Cloud Run will provide a URL for your deployed service.

### 3. Configure Domain and SSL

If you want to use a custom domain for your backend, you can map it to your Cloud Run service.

1.  **Map a custom domain:**
    - In the GCP Console, go to **Cloud Run**.
    - Select your `mitra-backend` service.
    - Click **Manage custom domains**.
    - Follow the instructions to add a domain mapping and verify domain ownership.

2.  **SSL Certificates:**
    - Cloud Run automatically provisions and renews SSL certificates for your custom domains, so you don't need to manage them manually.

### 4. Set Up Monitoring and Logging

- **Logging:** Cloud Run is integrated with **Cloud Logging**, so all `stdout` and `stderr` from your application are automatically collected and viewable in the GCP Console.
- **Monitoring:** Cloud Run is also integrated with **Cloud Monitoring**, which provides metrics like request count, latency, and container CPU/memory usage. You can set up alerts based on these metrics to be notified of any issues.

### 5. Configure Rate Limiting and Security Headers

- **Rate Limiting:** To prevent abuse, you can use a service like **Google Cloud Armor** to configure rate limiting rules for your Cloud Run service.
- **Security Headers:** You can add security headers (e.g., `Content-Security-Policy`, `Strict-Transport-Security`) to your responses by using a middleware in your FastAPI application.

By following these steps, you can deploy a scalable, secure, and reliable backend for the Mitra AI application.
