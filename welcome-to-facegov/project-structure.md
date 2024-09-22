# Project Structure

FaceGov uses AWS Lambda and other AWS services. Here's a brief explanation of how FaceGov Backend System is structured.

{% embed url="https://lucid.app/lucidchart/7dbcbb80-2ca1-424f-a30f-65cfc736def5/edit?invitationId=inv_4d9b9f6c-7e70-4f05-b652-77fa1c4d6ce9&page=0_0" %}

```
src/
|-- components/
|   |-- Icon.tsx
|   |-- Card.tsx
|   |-- Navigation.tsx
|   |-- Sidebar.tsx
|   |-- Feed.tsx
|   |-- RightSidebar.tsx
|   `-- Post.tsx
|-- pages/
|   |-- Home.tsx
|   |-- FactChecksPage.tsx
|   `-- UKMPsDiagram.tsx
|-- types/
|   `-- index.ts
|-- App.tsx
`-- index.tsx
```

1. API Gateway: Handles incoming HTTP requests and routes them to appropriate Lambda functions.
2. Lambda Functions: Implement the core business logic, such as:
   * User registration and authentication
   * Creating and retrieving posts
   * Managing user profiles
   * Implementing voting or rating systems
   * Handling comments and replies
3. DynamoDB: A NoSQL database to store user data, posts, comments, and other structured data.
4. S3: Store media files like images or videos that users might upload.
5. Cognito: Manage user authentication and authorization.
6. SNS (Simple Notification Service): Handle notifications for activities like new comments or replies.
7. Elasticsearch: Implement search functionality across posts and user profiles.
8. CloudWatch: Monitor your Lambda functions and other AWS services.
9. CloudFront: Content Delivery Network (CDN) to serve static assets and media files quickly.

This serverless architecture allows your application to scale automatically based on demand. Each Lambda function can handle a specific task, making the system modular and easier to maintain.
