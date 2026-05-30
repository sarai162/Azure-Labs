# Question (AWS Day 33)

The Nautilus DevOps team is embracing serverless architecture by integrating AWS Lambda into their operational tasks. They have decided to deploy a simple Lambda function that will return a custom greeting to demonstrate serverless capabilities effectively. This function is crucial for showcasing rapid deployment and easy scalability features of AWS Lambda to the team.

Create Lambda Function: Create a Lambda function named xfusion-lambda.

Runtime: Use the Runtime Python.

Deploy: The function should print the body Welcome to KKE AWS Labs!.

Status Code: Ensure the status code is 200.

IAM Role: Create and use the IAM role named lambda_execution_role.


# Solution

```

1. Open the AWS Console and go to IAM.
2. Create a new IAM role for Lambda and attach the basic Lambda execution permissions.
3. Go to AWS Lambda and choose Create function.
4. Create a new function with the required name.
5. Select Python as the runtime.
6. Assign the IAM role you created to the function.
7. Edit the function code so it returns the required message in the response body.
8. Set the response status code to 200.
9. Save and deploy the function.
10. Test the function to confirm it runs successfully and returns the expected output.

```
