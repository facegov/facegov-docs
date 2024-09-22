# Externalizing configuration

It's generally a good practice to externalize configuration values like these rather than hardcoding them in your application.  We'll use AWS Systems Manager Parameter Store to manage these values, which is a common practice for AWS Lambda functions.

This approach offers several benefits:

1. Flexibility: You can change these values without modifying and redeploying your code.
2. Security: Sensitive information (like API endpoints) can be managed separately from the code.
3. Environment-specific configuration: You can easily use different values for development, testing, and production environments.
