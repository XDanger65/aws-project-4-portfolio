# AWS Serverless Task Manager

A serverless REST API built with AWS Lambda, Amazon API Gateway, and Amazon DynamoDB using the AWS Serverless Application Model (AWS SAM).

## Architecture

- **Amazon API Gateway:** Exposes HTTP endpoints.
- **AWS Lambda:** Processes requests using Python 3.13.
- **Amazon DynamoDB:** Stores tasks persistently.
- **AWS SAM:** Defines, builds, and deploys the infrastructure.
- **AWS CloudFormation:** Manages the deployed stack.

Request flow:

`Client → API Gateway → Lambda → DynamoDB`

## Features

- Create tasks with a title and description.
- Retrieve saved tasks.
- Generate a unique ID for each task.
- Record task creation timestamps in UTC.
- Validate incoming JSON and required task titles.
- Grant Lambda access to DynamoDB through an IAM policy.

## API Endpoints

Base URL:

`https://plxuw3w49l.execute-api.us-east-1.amazonaws.com/Prod`

| Method | Endpoint | Description |
|---|---|---|
| GET | `/hello/` | Health-check-style greeting |
| POST | `/tasks` | Create a task |
| GET | `/tasks` | List tasks |

### Create a task

Send a `POST` request to `/tasks` with JSON:

```json
{
  "title": "Learn AWS Lambda",
  "description": "Practice serverless development"
}
```

A successful response returns the task ID, title, description, and creation timestamp.

### List tasks

Send a `GET` request to `/tasks` to retrieve stored tasks and their count.

## AWS Resources

- CloudFormation stack: `aws-project-4-portfolio`
- DynamoDB table: `aws-project-4-portfolio-tasks`
- Lambda logical resource: `HelloWorldFunction`
- AWS Region: `us-east-1`

## Deployment

Install and configure the AWS CLI and AWS SAM CLI, then run:

```powershell
sam validate
sam build
sam deploy
```

## Testing with PowerShell

```powershell
$apiUrl = "https://plxuw3w49l.execute-api.us-east-1.amazonaws.com/Prod/tasks"

$body = @{
    title = "My first AWS task"
    description = "Testing Lambda and DynamoDB"
} | ConvertTo-Json

Invoke-RestMethod -Uri $apiUrl -Method Post `
  -ContentType "application/json" -Body $body

Invoke-RestMethod -Uri $apiUrl -Method Get
```

Verify stored data directly:

```powershell
aws dynamodb scan `
  --table-name aws-project-4-portfolio-tasks `
  --region us-east-1
```

## Security and Cost Notes

- The Lambda function receives table access through an IAM policy.
- DynamoDB uses on-demand billing (`PAY_PER_REQUEST`).
- Review AWS resource usage and costs after testing.
- Do not commit AWS credentials, secret keys, or `.env` files.

## Future Improvements

- Add task update and delete endpoints.
- Add pagination to task listing.
- Add automated unit and integration tests.
- Add authentication and authorization.
- Add CI/CD with GitHub Actions.
- Add monitoring and alarms with Amazon CloudWatch.

## Author

Islam Mostafa

GitHub: [XDanger65](https://github.com/XDanger65)

