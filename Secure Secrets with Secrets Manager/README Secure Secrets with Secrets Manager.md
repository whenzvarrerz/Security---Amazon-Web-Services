<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Secure Secrets with Secrets Manager

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-secretsmanager)

**Author:** Wency Barrera  
**Email:** wencitybarrera@gmail.com

---

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-secretsmanager_r7s8t9u0)

---

## Introducing Today's Project!

In this project, I will:

✓ Determine how a web application is storing credentials unsafely.
✓ Explore how GitHutb's secret scanning feature prevents insecure code from being committed to a repository.
✓ Modify the web application to utilize AWS Secrets Manager for securely storing and accessing credentials. 
✓ Confirm that the updated web application code can be shared publicly without revealing sensitive credentials.

### Tools and concepts

Services I used were S3, GitHub, IAM, and Secrets Manager.

The key concepts I've learned were:

→ Phyton Virtual Environments (venv).
→ Fixing PowerShell Script Execution Issues.
→ Git Basics (Committing and Pushing).
→ GitHub Forking vs. Cloning.
→ GitHub Secret Scanning.
→ Git Rebasing
→  AWS Secrets Manager for Secure Credentials. 

### Project reflection

This project took me over 4 hours to finish, from learning the concepts, documentation, and taking the quiz. The most challenging part was configuring Python, PowerShell, and Git errors. 

It was rewarding because I was able to learn how to use GitHub and Python's virtual environment. 

I decided to work on this project today to achieve my goal of learning how to apply security measures to various AWS services. 

---

## Hardcoding credentials

Publicly exposing AWS credentials poses a significant security threat and is highly unsafe for production applications. If someone gains access to the credentials, they could compromise the AWS account, delete resources, steal sensitive data, or cause other harm. 

I've set up the initial configuration with these values:

AWS_ACCESS_KEY_ID = "AKIAW3MEFRAFTQM5FHKE"
AWS_SECRET_ACCESS_KEY = "F0b8s5m+pOZsttvBCirr1BOutuvCpqXMW2Y1qAxY"
AWS_REGION = "us-east-2"


These are sample AWS access keys. We're using these credentials because they're safer and simpler to work with than real ones, which could expose an account to security vulnerabilities. 


![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-secretsmanager_j2k3l4m5)

---

## Using my own AWS credentials

As an extension for this project, I set up a Python virtual environment to isolate and manage all the necessary packages for the web application. Additionally, I installed the required libraries listed in requirements.txt, boot3, fastapi, and uvicorn, to enable the application to run successfully. 

This is the error I received when trying to View My S3 Buckets: 

{"error":"An error occurred (InvalidAccessKeyId) when calling the ListBuckets operation: The AWS Access Key Id you provided does not exist in our records."}

This error indicates that the AWS Access Key ID used in the web application is invalid. Although the app is running, it cannot connect to your AWS account due to incorrect credentials. 

This issue arises because the placeholder credentials in config.py are not authentic AWS credentials. 

I updated the config.py by setting up my AWS security credentials in IAM Admin User.  

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-secretsmanager_wghjteykut)

---

## Pushing Insecure Code to GitHub

After updating the web app code with credentials, I forked the repository to make my own version of someone else's project in my GitHub account, so I can edit it freely while still keeping a link to the original project in case I want to share the changes back. Cloning is just downloading the project to your computer without creating a copy on GitHub.  

To connect my local repository to the forked repository, I run the git command git commit -m "Updated config.py with hardcoded credentials" to save changes I've made in the file. 

I also used the git push -u origin main, to upload changes from local repository to GitHub fork to test features like secret scanning. 



GitHub rejected my push due to an error message stating, "Push cannot contain secrets." GitHub's secret scanning feature automatically checks code for sensitive information, such as AWS credentials, and blocks the push if any are found. 

GitHub applied its security measure to protect against unintentionally exposing sensitive credentials on config.py containing AWS Access Key ID and Secret Access Key.  

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-secretsmanager_o2p3q4r5)

---

## Secrets Manager

AWS Secrets Manager is a specialized service designed to securely manage sensitive information, such as credentials ("secrets").

Secret rotation is the automatic, regular updating of sensitive credentials like passwords or API keys to enhance security. It reduces the risk of compromised secrets by limiting their validity period. 

Use secret rotation for critical credentials, such as database passwords, privileged API keys, or service account credentials, to minimize the potential damage from a compromise by frequently changing them.  

AWS Secrets Manager makes it simple for developers to work with their apps by offering a secure method to store, manage, and access sensitive data, such as API keys or database passwords, without embedding them directly in the application's code.  

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-secretsmanager_h2i3j4k5)

---

## Updating the web app code

I updated the config.py by deleting the old one and creating a new config.py with a Python code coming from AWS Sectets Manager  → Secrets → aws-access-key.

The new code handles fetching the credentials from the secret access key created and setting them to use. 

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-secretsmanager_v0w1x2y3)

---

## Rebasing the repository

Git rebasing is a process in Git that allows you to rewrite or reorganize the commit history of your repository by moving, modifying, or combining commits. Instead of adding new commits on top of your current branch, rebasing re-applies your commits onto a different base, creating a cleaner, more linear history. 

It's like rearranging the story of your project's changes to make it more organized or to fix mistakes. 

A merge conflict happened during rebasing because Git got confused. First, I committed to changes to remove hard-coded credentials . Then, I made additional changes to config.py. Git asked whether it should discard those changes as well. 

I resolved the merge conflict by manually editing the conflicting files. 

After updating the configuration file, I confirmed that my GitHub Fork no longer exposes credentials by reviewing the repository, which now uses code to retrieve credentials securely instead of the previously hard-coded ones. 

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-secretsmanager_t5u6v7w8)

---

---
