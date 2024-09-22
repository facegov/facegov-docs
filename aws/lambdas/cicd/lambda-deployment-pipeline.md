# Lambda Deployment Pipeline

Git Workflow for is used fro building and Deploying Java Lambda Functions



The `/.github/workflows/build.yml` GitHub Actions CI pipeline:

1. Build the project
2. Run unit tests
3. Run integration tests
4. Generate deployment artifacts (JAR file)

###

The pipeline is located in `.github/workflows/build.yml`&#x20;

This GitHub Actions workflow will build your Lambda function using Gradle and deploy it to AWS using a SAM template. Here's a breakdown of what this workflow does:

1. It triggers on pushes to the main branch.
2. Sets up Java 11 for the Gradle build.
3. Builds the project using Gradle.
4. Sets up Python and installs the AWS SAM CLI.
5. Configures AWS credentials using secrets stored in your GitHub repository.
6. Builds the SAM application.
7. Deploys the SAM application to AWS.

```yaml
name: Build and Deploy Java Lambda

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3

    - name: Set up JDK 11
      uses: actions/setup-java@v3
      with:
        java-version: '11'
        distribution: 'adopt'

    - name: Cache Gradle packages
      uses: actions/cache@v3
      with:
        path: ~/.gradle/caches
        key: ${{ runner.os }}-gradle-${{ hashFiles('**/*.gradle') }}
        restore-keys: ${{ runner.os }}-gradle

    - name: Build with Gradle
      run: ./gradlew build

    - name: Set up Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.x'

    - name: Install AWS SAM CLI
      run: |
        pip install aws-sam-cli

    - name: Configure AWS credentials
      uses: aws-actions/configure-aws-credentials@v1
      with:
        aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
        aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        aws-region: us-east-1  # Change this to your desired AWS region

    - name: SAM build
      run: sam build

    - name: SAM deploy
      run: sam deploy --no-confirm-changeset --no-fail-on-empty-changeset
```



To use this workflow, you'll need to:

1. Save this YAML file in your repository under `.github/workflows/`, for example as `deploy-lambda.yml`.
2. Store your AWS credentials as secrets in your GitHub repository:
   * Go to your repository settings
   * Click on "Secrets and variables" > "Actions"
   * Add `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` as secrets
3. Ensure you have a `template.yaml` (SAM template) file in your repository root.
4. Modify the AWS region in the workflow file if needed.
5. Make sure your Gradle build produces the artifacts expected by your SAM template.
