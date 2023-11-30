This Lambda function is designed to handle the submission of assignments triggered by an SNS event. It performs the following tasks:

Downloads the assignment content from a provided GitHub URL.
Uploads the content to Google Cloud Storage (GCS).
Notifies the user via email about the successful submission and provides the access URL for the uploaded assignment.
Logs relevant information and tracks submission status in DynamoDB.
Functionality
The Lambda function is triggered by an SNS event containing submission details such as the submission URL, user email, and assignment ID. It executes the following steps:

 1: Download from GitHub

Utilizes node-fetch to download the assignment content from the provided GitHub URL.
Validates the download status and throws an error if the URL is invalid or the file cannot be downloaded.

 2: Upload to Google Cloud Storage

Uses the @google-cloud/storage library to upload the downloaded content to Google Cloud Storage.
Generates a unique file name based on the user's email, assignment ID, and timestamp.
Returns the URL of the uploaded assignment in GCS.

 3: Send Email Notification

Sends an email notification to the user using the mailgun-js library to notify them about the successful submission.
Logs the submission status and tracks it in DynamoDB, updating the entry with a unique ID, email, timestamp, message content, status, and any error message encountered.
Dependencies
AWS SDK: Handles interactions with AWS services like DynamoDB.
node-fetch: Enables fetching resources from the GitHub URL.
@google-cloud/storage: Facilitates interaction with Google Cloud Storage.
mailgun-js: Sends email notifications using Mailgun API.
uuid: Generates unique identifiers for DynamoDB entries.
Environment Variables
Ensure the following environment variables are correctly set:

GCP_SERVICE_ACCOUNT: JSON string containing Google Cloud service account credentials.
GCS_BUCKET_NAME: Google Cloud Storage bucket name.
DYNAMODB_TABLE_NAME: Name of the DynamoDB table to track submission details.
MAILGUN_API_KEY: API key for Mailgun.
MAILGUN_DOMAIN: Mailgun domain.
