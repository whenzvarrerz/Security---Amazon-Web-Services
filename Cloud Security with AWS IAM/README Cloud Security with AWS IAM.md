<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Cloud Security with AWS IAM

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-iam)

**Author:** Wency Barrera  
**Email:** wencitybarrera@gmail.com

---

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-iam_1c864649)

---

## Introducing Today's Project!

For this project, I'll set up an EC2 Instance, IAM Policies, IAM Users, User Groups, and AWS Account Alias. I'll use the AWS Identity and Access Management (IAM) service to manage who can sign in (authentication) and what permissions they have (privilege) in my AWS account. 

### Tools and concepts

Services I used were the EC2 Instance and the IAM Policy. Key concepts I learnt include EC2 Instance is like a virtual computer in the cloud that runs your applications. IAM policy set the rules for what users and services can do with AWS resources.

Using IAM user groups makes it easier to manage permissions by grouping users with similar access needs together. Account aliases create a simple, easy to remember URL or users to log into the AWS Console Management, making it more convenient to share and use. 

### Project reflection

This project took me approximately five hours to complete. The most challenging part was identifying my error, which originated from the start of my EC2 and policy creation. 

It was most rewarding to see that, as a result, I was able to understand the concept better, the policy-tagging relationship. Don't hesitate to ask the right question to get the right answer. This also showed me that the NextWork community is always ready to help fellow learners.  

---

## Tags

Tags are labels that help organize resources. Tagging enables quick identification of all resources with the same tag and acts as a helpful filter when you are searching for specific items.  

The tag I’ve used on my EC2 instances are:
Name: network-prod-wency
Env: Production

Name: network-dev-wency
Env: Development

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-iam_2e0e5a5d)

---

## IAM Policies

An IAM Policy defines permissions for your AWS resources, specifying what actions IAM users, groups, or roles can or cannot perform on particular resources and when these permissions apply.  

### The policy I set up

For this project, I’ve set up a policy using JavaScript Object Notation, JSON. 

I’ve created a policy that allows certain actions for the EC2 instance, to start, stop and describe it. 

### When creating a JSON policy, you have to define its Effect, Action and Resource.

The Effect, Action, and Resource attributes of a JSON policy mean 'Effect' determines whether the policy allows or denies access, 'Action' specifies the operation, and 'Resource' specifies the AWS resource. 

---

## My JSON Policy

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-iam_1c864649)

---

## Account Alias

An account alias is a custom name for your AWS account that replaces the account ID (strings of numbers) for signing in to the AWS Management Console. 

Creating an alias simplifies remembering and sharing the AWS console login URL to other users. 

Creating an account alias took me less than a minute. Now, my new AWS console sign-in URL is https://network-alias-wency.signin.aws.amazon.com/console

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-iam_0eb4439b)

---

## IAM Users and User Groups

### Users

IAM users are individuals who are granted access to your AWS account and its resources. 

### User Groups

An IAM user group is a container for multiple IAM users, enabling you to manage permissions for all users in the group simultaneously by assigning policies to the group instead of each user individually. 

I attached the policy I created to this user group, which means the policy grants the trainees full permission to perform all possible actions to the EC2 instance Development. And also, limiting their resources within the defined scope. 

---

## Logging in as an IAM User

The first way is to share the AWS Management Console sign-in URL, user name, with console password, or send user email sign-in instructions on how to sign into the AWS Management Console. 

Once I logged in as an IAM user, I noticed some of my dashboard panels were showing Access denied because I have a limited scope of access.  

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-iam_6f2ab446)

---

## Testing IAM Policies

I tested my JSON IAM policy by stopping the two instances. My policy is only applicable to my  Development instance, allowing me to start and stop it. The Production instance is not included in this policy, so stopping it gave me an unauthorized error.    

### Stopping the production instance

When I attmepted to stop the production instance, I received a prompt stating I lack authorization to perform this action. 

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-iam_0e7a9d6a)

---

## Testing IAM Policies

### Stopping the development instance

I was able to stop the development instance. This was because the policy allows the actions to start, stop, and describe the EC2 instance.

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-iam_1811801c)

---

## The IAM Policy Simulator

### How I used the simulator

---

---
