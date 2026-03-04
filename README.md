In real AWS environments, unused resources don’t scream for attention — they silently burn money.

Old EBS volumes, stopped instances, unused snapshots… all of them slowly increase your monthly bill.

In this project , I  designed a  real production-style automation to detect idle (zombie) AWS resources and track them automatically — without manual audits.


 what i have build in this project 

An event-driven cleanup detection system that:

Detects idle EBS volumes
Stores idle resource data in DynamoDB
Sends alerts using SNS
Runs automatically on a schedule
Requires zero manual intervention

Perfect for  cost optimization tasks.

 🧱 Architecture Overview

```
EventBridge (Scheduled)
        ↓
AWS Lambda
        ↓
EC2 / EBS Scan
        ↓
DynamoDB (ZombieResourceTracker)
        ↓
SNS (Email Notification)
```


 🛠️ Step-by-Step Phases

Phase 1 – Prepare Test Resources

Create an idle EBS volume
Create DynamoDB table
  `ZombieResourceTracker`
Create SNS topic for notifications

Phase 2 – IAM Role for Lambda

Attach required permissions:

AWSLambdaBasicExecutionRole
AmazonSNSFullAccess
AmazonDynamoDBFullAccess
AmazonEC2FullAccess

Phase 3 – Lambda Function

Create Lambda function
Add environment variables:

  `TABLE_NAME`
  `SNS_TOPIC_ARN`
Lambda scans for idle EBS volumes and records findings

Phase 4 – EventBridge Automation

Create a scheduled EventBridge rule
Trigger Lambda automatically (daily / hourly)

 🎯 Why This Matters in Real Projects

Cloud bills grow silently
Manual audits don’t scale
Cost optimization is a core DevOps responsibility
This setup gives you audit evidence + alerts + automation
