<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Encrypt Data with AWS KMS

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-kms)

**Author:** Wency Barrera  
**Email:** wencitybarrera@gmail.com

---

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-kms_w0x1y2z3)

---

## Introducing Today's Project!

In this project, I will...

✓ Create and manage encryption keys in KMS.
✓ Encrypt a DynamoDB table using an encryption key. 
✓ Add data to the encrypted table.
✓ Use a test user to validate your encryption.
✓ Give your test user encryption access. 


### Tools and concepts

Services I used include AWS IAM (Identity and Access Management): This service helps you control who can access your AWS resources, by setting permissions. 
✓ Here, I created a test user and managed its access.

AWS KMS (Key Management Service): KMS is like a secure safe for encryption keys. 
✓ I learned how it creates and manages keys to lock (encrypt) and unlock (decrypt) data, ensuring only authorized users can access it. 

AWS DynamoDB: This is a fast and flexible AWS database for storingdata.
✓ I saw how it works with encryption to protect data.

Encryption: It scrambles data into a format (ciphertext) that needs a key to read. 
✓ I used symmetric encryption, which is fast and uses one key for both locking and unlocking data in DynamoDB. 

Decryption Permissions
✓ Seeing KMS key doesn't mean a user can decrypt data, they need specific permissions to do so, adding extra security. 



 ... Key concepts I learnt include encryption, ...'

### Project reflection

This project took me over two hours to grasp the concepts, document notes, and complete the quiz. I'm excited to have successfully set up AWS IAM, DynamoDB, and KMS, adding a few more services to my skill set. 

I decided to work on this project today to achieve my goal of learning how to apply security measures to various AWS services. 

---

## Encryption and KMS

Encryption transforms data into a secure, unreadable format known as ciphertext using algorithms. Only authorized users can decrypt it back to its original, readable form. 

An encryption key is used by an algorithm to determine how to convert plain text into a scrambled format called ciphertext. 

For example, the key might instruct the algorithm to replace specific data parts or rearrange the data order to disrupt patterns. 



AWS KMS, Key Management Service is a secure placement for your encryption keys. You use it to create, store, and manage these keys, which act like a secret code to protect your data in your AWS tools and services. 

Key management systems are important because it helps to keep your data safe from unauthorized access,, being stolen, or misused. 

Symmetric encryption uses a one secret key to both encrypt (lock) and decrypt (unlock) your data. It's like using the same key for a lock to secure and open it. 

✓ This method is super fast and works great for protecting big chunks of data, which is why we are using it for our DynamoDB table.

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-kms_a2b3c4d5)

---

## Encrypting Data

DynamoDB is a database service from AWS. It's a speedy and adaptable way to store data, making it perfect for applications that need to quickly access lots of information. 


The different encryption options in DynamoDB include:

Aws Owned Key: This is a secret key that DynamoDB owns and takes care of completely. It's like a lock that DynamoDB manages for you, and you don't have to pay extra.

AWS Managed Key: This is a secret key stored in your AWS account, but AWS Key Management Service KMS handles it for you. It's like a lock you own, but someone else manages, and you'll need to pay a fee for using KMS.

Customer Managed Key: This is a secret key that you store in your AWS account and control yourself. It's like a lock you own and manage, but you'll still pay a fee for using AWS KMS to help store it. 

Their differences are based on who owns and who manages the key. Who only has the visibility, who only has controI, or who has both the visibility and control.

I selected Customer Managed Keys because I want to have both control and visibility. 

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-kms_q8r9s0t1)

---

## Data Visibility

Instead of limiting who can see the KMS key, AWS KMS allows multiple users to access it, but only those with specific permissions can use it for actions like encrypting and decrypting data. 

The table is encrypted, but I have the permission to use the encryption key in AWS KMS. When you or an authorized application request data, DynamoDB automatically decrypts it using the key and shows it in a readable format, a process called transparent data encryption. 

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-kms_c0d1e2f3)

---

## Denying Access

On the navigation pane, I click “Users” → Create Users → Assign a user name → Tick box – “Provide user access to the AWS Management Console” → Set to skip resetting the password when logging in as user → Attach existing policies directly → Create user. 

The permission policies I granted this user are full access to the DynamoDB, but not to the KMS key.

When I tried accessing the DynamoDB table as a test user, I got an error saying the user isn't allowed to decrypt the data. This shows that while the test user can see the KMS key exists in the AWS environment, they don't have permission to decrypt the data it secures. 

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-kms_w0x1y2z3)

---

## EXTRA: Granting Access

I modified the key policy by adding key users. 

Using the test user dashboard, I went back and refreshed it. After that, I can see that the test user can now access the database's items.  

Use encryption to protect the actual data within the resrouce, like DynamoDB table, so even if someone bypasses access controls, such as anauthorized access of server or data interception, they can't read it without the decription key, ensuring strong data security.

In contrast, access control tools like security groups and permission policies manage who can access a resource or service, like DynamoDB, but they don't safeguard the data inside. Once someone has access, they can view or potentially misuse all the data they're permitted to see. 

![Image](http://learn.nextwork.org/soothed_purple_vibrant_yak/uploads/aws-security-kms_feffb2fb8)

---

---
