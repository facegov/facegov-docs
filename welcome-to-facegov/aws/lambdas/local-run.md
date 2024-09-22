# Local Run

1.  create a `.env.local` file in your project root with your development Cognito details. This file should not be committed to Git.

    ```
    CopyREACT_APP_USER_POOL_ID=your_dev_user_pool_id
    REACT_APP_CLIENT_ID=your_dev_client_id
    ```

This approach allows you to:

* Keep your sensitive data out of your codebase
* Use different configurations for different environments (dev, staging, prod)
* Automate your build and deployment process securely
