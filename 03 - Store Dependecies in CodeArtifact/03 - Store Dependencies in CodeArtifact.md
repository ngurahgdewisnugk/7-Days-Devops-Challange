<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# 🔐 Secure Packages with CodeArtifact

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-codeartifact-updated)

**Author:** Ngurah Gede Wisnu Gudakesa  
**Email:** ngurahgedewisnugk@gmail.com

---

![Image](http://learn.nextwork.org/motivated_teal_shy_hog/uploads/aws-devops-codeartifact-updated_1d79e699)

---

## 🚀 Introducing Today's Project!

In this project, I will set up **AWS CodeArtifact** as a secure repository for my web app's packages. My goal is to learn how to manage and store these packages in one central location, which is a crucial step for building robust CI/CD pipelines that ensure verified package versions are used during app building and deployment.

## 🛠️ Key Tools and Concepts

### Services Used

| Service | Purpose |
|---------|---------|
| **EC2 Instance** | Development environment and to host web app files |
| **GitHub Repository** | Version control and public code management |
| **IAM Services** | Secure permissions configuration for EC2 to access CodeArtifact |
| **CodeArtifact** | Central, secure repository for managing project dependencies |

### Key Concepts Learned

I learned how to effectively manage and store software packages in a central location using CodeArtifact. This is crucial for building robust CI/CD pipelines because it ensures that only verified package versions are used during application builds and deployments. By having a reliable source for dependencies, I can streamline development and maintain consistency across environments.

## 💭 Project Reflection

> **Time Investment:** ~3 hours

### Challenges Faced

The most challenging part was creating the IAM Policy for CodeArtifact access and setting up the AWS CodeArtifact Repository from scratch, as I needed more time to fully grasp these concepts.

### Most Rewarding Moment

It was most rewarding to successfully connect Maven with CodeArtifact and understand its role in securing package dependencies for CI/CD.

> 📌 **Note:** This project is part three of a series of DevOps projects where I'm building a CI/CD pipeline! I'll be working on the next project on the next day.

---

## 📦 CodeArtifact Repository

![alt text](<Assets/AWS CodeArtifact.png>)

AWS CodeArtifact is a fully managed artifact repository service that organizations use to securely store, publish, and share software packages and build tools. 

### Why It's Crucial for Engineering Teams

It provides a safe and secure central repository for all their dependencies. This ensures everyone on the team uses the same, verified versions of packages, which is especially important in a CI/CD pipeline to prevent issues like "works on my machine" problems and reduce security risks.

### Understanding CodeArtifact Domains

A **CodeArtifact domain** acts like a central container for multiple repositories. It helps manage them by providing a single place to set permissions and security settings that apply to all repositories within it, ensuring consistent access control without needing to configure each one separately.
> 🏷️ **My Domain:** `nextwork`

### Upstream Repository

An **upstream repository** acts as a backup source for packages that your CodeArtifact repository doesn't yet contain. When your application needs a package, CodeArtifact first checks its own storage. If it's not there, it then looks to the upstream repository to fetch it and stores a copy for future use.

> 🔗 **Upstream Repository:** Maven Central (popular public repository for open-source Java libraries)

![Image](http://learn.nextwork.org/motivated_teal_shy_hog/uploads/aws-devops-codeartifact-updated_n4o5p6q7)

---

## 🔒 CodeArtifact Security

### ⚠️ Issue

![alt text](<auth failed.png>)

I need an authorization token to access CodeArtifact because it acts like a temporary password for our development tools, such as Maven, to securely interact with my CodeArtifact repositories. 

**Initial Problem:**
- EC2 instance doesn't have permission to access CodeArtifact by default
- Encountered an `Unable to locate credentials` error when trying to retrieve a token
- This is a security feature based on the **principle of least privilege** in AWS

### ✅ Resolution

1.  I resolved the security token error by first creating an IAM Policy (`codeartifact-
    nextwork-consumer-policy`) that grants specific CodeArtifact permissions (get authorization token, repository endpoint, read from repository), adhering to the principle of least privilege. 
2. Then, I created an IAM Role (`ec2-instance-nextwork-cicd`) for my EC2 instance and attached this policy to it. 
 
3. Finally, I attached this IAM Role to my EC2 instance and re-ran the export token command. This succeeded ✅ because the EC2 instance now had the necessary permissions to securely access CodeArtifact through the assigned role.
![alt text](<auth success.png>)

### Why IAM Roles Are Best Practice

IAM roles are considered a security best practice because they:

- ✅ Enhance security and scalability by eliminating hardcoded credentials
- ✅ Automatically provide and rotate temporary security credentials
- ✅ Allow applications to automatically use temporary credentials for AWS API calls
- ✅ Eliminate the need to manually manage or store sensitive credentials
- ✅ Align with the principle of least privilege

---

## 📄 The JSON policy attached to my role

The IAM policy grants permissions for my EC2 instance to interact with CodeArtifact. Specifically, it allows the instance to:
	
#### Permissions Granted

1. **Get Authorization Tokens**
   - Temporary passwords for Maven to authenticate with CodeArtifact

2. **Find Repository Locations**
   - Enables EC2 instance to locate where packages are stored

3. **Read Packages from Repositories**
   - Crucial for Maven to fetch dependencies for my application

4. **Get Service Bearer Token**
   - From AWS Security Token Service (STS)
   - Provides temporarily elevated access for CodeArtifact operations

> 🔐 These permissions are necessary because my EC2 instance needs to securely connect to CodeArtifact so that Maven can authorize and access my package repositories.

![Image](http://learn.nextwork.org/motivated_teal_shy_hog/uploads/aws-devops-codeartifact-updated_23rp7q8r9)

---

## Maven and CodeArtifact

### To test the connection between Maven and CodeArtifact, I compiled my web app using `settings.xml`

The `settings.xml` file configures Maven by acting as its central control center. It tells Maven : 
1. Where to find project dependencies (specifically in my CodeArtifact repository)
2. How to authenticate to access them. 

This creates a seamless connection, allowing Maven to automatically authenticate and pull dependencies from the right, secure location across all my projects, without me needing to configure it repeatedly.

### What is Compiling?

Compiling is like translating my project's code into a language that computers can understand and run. When I compile my project with Maven:

1. Maven makes sure everything is correctly set up
2. Turns code into a working app
3. Stores dependencies in CodeArtifact Repository


![Image](http://learn.nextwork.org/motivated_teal_shy_hog/uploads/aws-devops-codeartifact-updated_c17eace8)

---

## ✅ Verify Connection

After compiling my web app, I checked my CodeArtifact Repository and saw multiple pages of packages. This tells me that:

1. ✅ Maven compile command successfully identified project dependencies from `pom.xml`
2. ✅ Dependencies weren't in CodeArtifact yet
3. ✅ CodeArtifact fetched them from Maven Central (upstream repository)
4. ✅ Cached them in my repository
5. ✅ Provided them to Maven

> 🎉 **Success!** This is proof that the entire system is working as expected!

![Image](http://learn.nextwork.org/motivated_teal_shy_hog/uploads/aws-devops-codeartifact-updated_1d79e699)
