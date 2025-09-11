<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Threat Detection with GuardDuty

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-guardduty)

**Author:** Wency Barrera  
**Email:** wencitybarrera@gmail.com

---

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-guardduty_v1w2x3y4)

---

## Introducing Today's Project!

### Tools and concepts

The services I used were:

✓ AmazonGuardDuty
✓ Amazon CloudFront
✓ Amazon S3
✓ CloudFormation
✓ OWASP Juice Shop.

Concepts I learned are:
→ Linux commands
→ SQL command injection
→ Malware protection 




### Project reflection

This project took me over three hours to complete from understanding the concepts, note taking for documentation, and taking the quiz.  The most rewarding part is seeing how GuardDuty is triggered to work. 

I want to finish the AWS Security project to learn how it works. My goal will be achieved if I can complete all five parts and fully grasp the concepts behind the services.  

---

## Project Setup

To set up this project, I deployed CloudFormation template that launches a web application for security training, the OWASP Juice Shop. 

The three main components are:
1. Web application infrastructure
→ EC2 Instance
→ Networking resource, new VPC
→ CloudFront Distribution - deployed to speed up web application creation.

2. S3 bucket for storage. 
3. GuardDuty for security monitoring. 

The web application hosted on CloudFront follows the OWASP Top 10. I will use GuardDuty to monitor these vulnerabilities, which I plan to test for exploitation. 

AWS GuardDuty is a security service that detects potential threats or attacks in your applications and AWS environment. It leverages machine learning to identify abnormal network activity. When it detects anything suspicious, it sends alerts to prompt further investigation. 

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-guardduty_n1o2p3q4)

---

## SQL Injection

The first attack I performed on the web app is SQL injection, which is a flaw in a website that lets an attacker add harmful SQL code to the database queries. 

This poses a security risk because these can allow attackers to skip login checks, steal information, or even change the database. 



My SQL injection includes the SQL query used for logging in. The part 'or 1=1-- makes the query always true, so you can bypass the login check. The SQL injection is set up to accept any password. 

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-guardduty_h1i2j3k4)

---

## Command Injection

Command injection is a major security flaw where the web server runs your commands when it should only save them. 

I performed the command injection by pasting JavaScript code in the Username field. This script will send instructions to the web application server (EC2 Instance). These instructions grab sensitive information (AWS IAM credentials) and save it where anyone online can see it.   

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-guardduty_t3u4v5w6)

---

## Attack Verification

To verify the vulnerability success, I used the URL of the hosted web app and appended:  /assets/public/credentials.json.

The credential page displayed the private key credentials that the web application developer is using to store its information.  These are web application's key to access AWS resources in the developer's account. 



![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-guardduty_x7y8z9a0)

---

## Using CloudShell for Advanced Attacks

The attack continues in CloudShell, and we will use this to run the commands that an intruder would use to steal data from the AWS environment. 

I ran the wget command to download the credentials.json file from the web application into CloudShell. This creates a local file CloudShell with the stolen credentials. 

The cat command shows the contents of that file, and the jq command makes the JSON data inside easier to read. 

I am viewing the stolen credentials from the credentials.json. file.  

We're creating a new profile called "stolen" in CloudShell to use the credentials we took from the web app attack. This allows us to look for vulnerabilities into our AWS environment, and we'll check if GuardDuty can detect the actions we're going to perform.  

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-guardduty_j9k0l1m2)

---

## GuardDuty's Findings

After carrying out the attack, GuardDuty reported the issue within 15 minutes. Findings are alerts from GuardDuty that flag suspicious activity and provide details about who, what, and when the attack occurred. 

GuardDuty finding was called UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration.InsideAWS, the credentials for my  EC2 instance were used in a different account. Anomaly detection flagged this because it was unusual activity. 

GuardDuty's detailed report showed that the S3 bucket was impacted. It identified the action taken with the stolen credentials, the EC2 instance, whose credentials were exposed, and the IP addresses and location of the attacker. 

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-guardduty_v1w2x3y4)

---

## Extra: Malware Protection

For my project extension, I enabled the Malware Protection for my S3 bucket in the GuardDuty console. Malware is malicious software that is desgined to harm computers.

I uploaded the EICAR test file to test Malware Protection. This is a safe file designed to trick antivirus software into thinking it's a malware.

It acts like a pretend virus to check if your antivirus is functioning correctly without using a real virus. In this case, we're using it to test if GuardDuty can spot malware.

After uploading the malware, GuardDuty immediately flagged it with a finding labeled Object:S3.MaliciousFile. This confirmed that GuardDuty successfully detected the malware. It also noted that the threat type was EICAR-Test-File. 

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-guardduty_sm42x3y4)

---
