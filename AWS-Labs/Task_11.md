# Question (AWS Day 34)

The Nautilus DevOps team continues to explore serverless architecture by setting up another Lambda function. This time, the task must be completed using the AWS Console to familiarize the team with the web interface. The function will return a custom greeting and demonstrate the capabilities of AWS Lambda effectively.

Create Python Script: Create a Python script named lambda_function.py with a function that returns the body Welcome to KKE AWS Labs! and status code 200.

Zip the Python Script: Zip the script into a file named function.zip.

Create Lambda Function: Create a Lambda function named devops-lambda-cli using the zipped file and specify Python as the runtime.

IAM Role: Use the IAM role named lambda_execution_role.


# Solution (aws-client-terminal)

```

aws-client ~ ➜  echo "def lambda_handler(event, context):
    return {
        'statusCode': 200,
        'body': 'Welcome to KKE AWS Labs!'
    }" > lambda_function.py

aws-client ~ ➜  ls
lambda_function.py

aws-client ~ ➜  cat lambda_function.py 
def lambda_handler(event, context):
    return {
        'statusCode': 200,
        'body': 'Welcome to KKE AWS Labs!'
    }

aws-client ~ ➜  zip function.zip lambda_function.py
  adding: lambda_function.py (deflated 14%)

aws-client ~ ➜  ls
function.zip  lambda_function.py

aws-client ~ ➜  ROLE_ARN=$(aws iam get-role --role-name lambda_execution_role --query 'Role.Arn' --output text)

aws-client ~ ➜  aws lambda create-function \    --function-name devops-lambda-cli \
    --runtime python3.9 \
    --role $ROLE_ARN \
    --handler lambda_function.lambda_handler \
    --zip-file fileb://function.zip
{
    "FunctionName": "devops-lambda-cli",
    "FunctionArn": "arn:aws:lambda:us-east-1:726851244429:function:devops-lambda-cli",
    "Runtime": "python3.9",
    "Role": "arn:aws:iam::726851244429:role/lambda_execution_role",
    "Handler": "lambda_function.lambda_handler",
    "CodeSize": 293,
    "Description": "",
    "Timeout": 3,
    "MemorySize": 128,
    "LastModified": "2026-05-27T06:39:26.637+0000",
    "CodeSha256": "N0LgLps9oKsYrxfHHfPyVMRyKeS4LHEgeJTqA3PcGlw=",
    "Version": "$LATEST",
    "TracingConfig": {
        "Mode": "PassThrough"
    },
    "RevisionId": "e5bcec72-961a-4b4d-89dd-a1b744aafdee",
    "State": "Pending",
    "StateReason": "The function is being created.",
    "StateReasonCode": "Creating",
    "PackageType": "Zip",
    "Architectures": [
        "x86_64"
    ],
    "EphemeralStorage": {
        "Size": 512
    },
    "SnapStart": {
        "ApplyOn": "None",
        "OptimizationStatus": "Off"
    },
    "RuntimeVersionConfig": {
        "RuntimeVersionArn": "arn:aws:lambda:us-east-1::runtime:b46f7bc0f3da8071d1b824471f2c69c8766b756b827eb0455d2118c622ae7bcf"
    },
    "LoggingConfig": {
        "LogFormat": "Text",
        "LogGroup": "/aws/lambda/devops-lambda-cli"
    }
}

aws-client ~ ➜  aws lambda invoke --function-name devops-lambda-cli output.json
{
    "StatusCode": 200,
    "ExecutedVersion": "$LATEST"
}

aws-client ~ ➜  cat output.json
{"statusCode": 200, "body": "Welcome to KKE AWS Labs!"}
aws-client ~ ➜  

```
