# Lambda Local Dev

This page explain how to set up  AWS SAM CLI for Java Lambda Testing

### Prerequisites

* Java Development Kit (JDK) 11 or later
* IntelliJ IDEA
* Docker
* AWS SAM CLI

### Steps

1. Install AWS SAM CLI: Follow the official AWS guide to install SAM CLI: [https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html)
2.  Create a SAM project (if you haven't already):

    ```
    Copysam init --runtime java11 --dependency-manager gradle
    ```
3. Open the project in IntelliJ IDEA.
4.  Create a `template.yaml` file in your project root if it doesn't exist:

    ```yaml
    yamlCopyAWSTemplateFormatVersion: '2010-09-09'
    Transform: AWS::Serverless-2016-10-31
    Description: SAM Template for Java Lambda function

    Resources:
      MyJavaLambda:
        Type: AWS::Serverless::Function
        Properties:
          Handler: com.example.App::handleRequest
          Runtime: java11
          CodeUri: .
          Events:
            HelloWorld:
              Type: Api
              Properties:
                Path: /hello
                Method: get
    ```
5. Modify your Lambda function code as needed.
6.  Build your project:

    ```
    Copy./gradlew build
    ```
7.  Use SAM CLI to run your function locally:

    ```
    Copysam local invoke MyJavaLambda --event events/event.json
    ```
8.  For API Gateway-triggered functions, you can start a local API:

    ```
    Copysam local start-api
    ```
9.  Test your API using curl or a web browser:

    ```
    Copycurl http://localhost:3000/hello
    ```

### Debugging with IntelliJ

1.  Run SAM CLI with the debug option:

    ```
    Copysam local invoke MyJavaLambda --event events/event.json -d 5858
    ```
2. In IntelliJ, create a "Remote" debug configuration:
   * Run > Edit Configurations > Add New Configuration > Remote
   * Set Name: "Debug SAM Lambda"
   * Host: localhost
   * Port: 5858
3. Set breakpoints in your code.
4. Start the debug session in IntelliJ.
5. The Lambda function will pause at your breakpoints when invoked.
