# SCTP2-14_Assignment 

## Does SNS guarantee exactly-once delivery to subscribers?
No, Amazon SNS (Simple Notification Service) does not guarantee exactly-once delivery. It follows an at-least-once delivery model, meaning messages may be delivered more than once to subscribers. This can happen due to retries, network failures, or other system behaviors. If exactly-once processing is required, the subscriber must implement idempotency to handle duplicate messages.

## What is the purpose of the Dead-letter Queue (DLQ)?
A Dead-letter Queue (DLQ) is used in Amazon SQS, SNS, and EventBridge to capture messages that fail to be processed successfully after a defined number of retry attempts. The main purposes of a DLQ are:

- Prevent message loss by storing undeliverable messages.
- Allow debugging and troubleshooting failed messages.
- Provide a mechanism to analyze and fix issues in message processing.

## How would you enable a notification to your email when messages are added to the DLQ?
To receive email notifications when messages are added to a DLQ, follow these steps:

1. Create an SNS Topic (e.g., DLQAlerts)
2. Subscribe an Email Address to the SNS Topic.
3. Create an AWS Lambda Function to monitor the DLQ and publish messages to the SNS Topic.
4. Trigger the Lambda Function from the DLQ using an event source mapping (for SQS-based DLQs).
5. Deploy the Lambda Function, which will send alerts to the SNS Topic when messages are added to the DLQ.

Alternatively, you can use CloudWatch Alarms to monitor the ApproximateNumberOfMessages metric for the DLQ and trigger an SNS notification when messages accumulate.
