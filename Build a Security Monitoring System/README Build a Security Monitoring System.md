<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a Security Monitoring System

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-monitoring)

**Author:** Wency Barrera  
**Email:** wencitybarrera@gmail.com

---

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-monitoring_reghtjy)

---

## Introducing Today's Project!

In this project, I will demonstrate: 
✓ Configure AWS CloudTrail to monitor secret access events.
✓ Recording access attempts and enabling notifications.
✓ Setting up SNS alerts to receive notifications when secrets are accessed.
✓ Develop a second notification system and evaluate which method provides more effective security alerts.

### Tools and concepts

In this project, I learned to:

✓ Use AWS Secrets Manager to securely store and manage secrets.
✓ Enable AWS CloudTrail to log secret access.
✓ Check security events in CloudTrail Event History and S3 logs.
✓ Create CloudWatch Metric Filters to track secret access.
✓ Set up CloudWatch Alarms and SNS notifications for real-time alers. 

### Project reflection

This project took me more than two hours to understand the concept of each service, creating documentation, and taking the quiz. 

---

## Create a Secret

AWS Secrets Manager safeguards sensitive data, such as passwords, API keys, credentials, and other confidential information.  

For my project setup in AWS Secrets Manager, I generated a secret named TopSecretInfo, which I will track for access monitoring.

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-monitoring_o5p6q7r8)

---

## Set Up CloudTrail

CloudTrail is a monitoring service that records all actions in your AWS account, tracking, who, what, when, and where. This ongoing logging aids security by detecting odd activity, supports troubleshooting by identifying changes, and ensures compliance by verifying rule adherence. 

A trail instructs CloudTrail on which activities to monitor and where to store the logs. 

CloudTrail events include types like:
Management events - track admin actions configuring AWS resources, like creating EC2 instances, updating security groups, or accessing secrets.

Data events - monitor high-volume actions on resources, such as uploading files to S3 or executing Lambda functions.

Insight events - identify unusual patterns in management events, like a sudden spike in IAM user creation. 

Network activity events - record network-related changes, such as VPC configuration updates or subnet traffic. 

### Read vs Write Activity

Read API activity tracks non-modifying actions, like S3 buckets, describing EC2 instances, or viewing secret metadata. 

Write API activity monitors changes, such as creating, deleting, or modifying resources, or retrieving a secret's value, which we aim to track. 

---

## Verifying CloudTrail

I retrieved the secret in two ways: First, through AWS Secret Manager Secret's dashboard. 

Second using  CloudShell with this command: 
aws secretsmanager get-secret-value --secret-id "TopSecretInfo" --region your-region-code




To analyze my CloudTrail events, I went to the events related to secretmanager.amazonaws.com, browsed through the event list, and looked for an event named GetSecretValue. This event indicates that my secret's value was accessed or retrieved.  

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-monitoring_s8t9u0v1)

---

## CloudWatch Metrics

CloudWatch Logs is an AWS service that collects, stores, and analyzes log data from applications and AWS resources. It's important for monitoring because it helps track system performance, detect issues, and troubleshoot problems by providing detailed insights into application and infrastructure activity. 

CloudTrail's logs AWS API calls and user activity for auditing and compliance, while CloudWatch logs stores and analyzes application and system logs for monitoring and troubleshooting. 

A CloudWatch metric value records a count (set to 1) each time a filter detects a secret access in the logs, while a default value (set to 0) is recorded when no access is detected, ensuring all time periods are shown on charts for a complete view of access activity. 

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-monitoring_a9b0c1d2)

---

## CloudWatch Alarm

My threshold alarm determines when the alarm activates. I'm configuring a static threshold to trigger the alarm when the SecretIsAccessed metric reaches or exceeds 1 within a 5-minute period.

An SNS (Simple Notification Service) topic acts like a messaging hub for notifications. You first set up the topic, then add subscribers (like email), and when you send a message to the topic, SNS instantly distributes it to all subscribers. 

AWS requires email confirmation for SNS subscription to verify that it's really you requesting the alerts. You'll need to check your email inbox and confirm your subscription to the alarm. 

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-monitoring_fsdghstt)

---

## Troubleshooting Notification Errors

To test my monitoring system, I accessed my secret value in AWS Secrets Manager and expected an email alert to confirm it was accessed, but no email notification arrived. 

When troubleshooting the notification issues:

1. Verify that CloudTrail is capturing the GetSecretValue event logs.
2. Ensure CloudTrail is properly configured to send logs to CloudWatch. 
3. Confirm that the CloudWatch metric filter is correctly set up to detect relevant log events.
4. Check that the CloudWatch Alarm is configured to trigger an action when conditions are met. 
5. Validate that SNS is correctly delivering email notifications to the assigned email address.  

I initially didn't receive an email before because I disabled the SNS. 

---

## Success!

To validate that my monitoring system works, I accessed my AWS Secrets Manager, Secrets, and retrieve the secret value again. I returned to the CloudWatch console, refreshed the "Secret is accessed" alarm, and confirmed it was in the "In alarm" state. 

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-monitoring_ageraergearge)

---

## Comparing CloudWatch with CloudTrail Notifications

I updated my CloudTrail configurations to enable SNS notifications, which send alerts to my SNS topic whenever a new log file is delivered to my S3 bucket. This differs from my CloudWatch Alarm, which only activates when a specific event, like accessing your secret, is detected in the logs. 

After enabling CloudTrail SNS notification, I have emails on my inbox regarding this feature. This ongoing emails will persis as long as the SNS notification setting is active and there's any activity in my AWS account.

Note that CloudTrail batches events every 5-15 minutes, creating a new log file each time, which triggers SNS notification. Since CloudTrail logs all management events in my AWS account - not just secret access, this results in multiple log files and, consequently, multiple notifications. 

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-monitoring_d7e8f9g0)

---

---
