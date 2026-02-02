<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Set Up a Web App in the Cloud

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-vscode)

**Author:** Ngurah Gede Wisnu Gudakesa  
**Email:** ngurahgedewisnugk@gmail.com

---

## Set Up a Web App Using AWS and VS Code

![Image](http://learn.nextwork.org/motivated_teal_shy_hog/uploads/aws-devops-vscode_7a1de541)

---

## Introducing Today's Project!

In this project, I will set up a basic web app server in the cloud using an EC2 instance and VS Code. I'm doing this to learn the foundational steps for building and preparing a web application, which is the first step in shipping software to users.


This project is part one of a series of DevOps projects where I'm building a CI/CD pipeline! I'll be working on the next project, Connect a GitHub Repo with AWS, soon.

I chose this project because it directly aligns with my goal of transitioning into Cloud Native Orchestration, particularly with AWS. I'm enthusiastic about this area because these skills are highly in-demand, and this project helps build foundational knowledge for CI/CD pipelines.


### Key tools and concepts

Services I used were : 
1. IAM to setup IAM user, 
![alt text](<assets/IAM User.png>)
2. EC2 instance for virtual server, 
3. VS Code for editor on my local computer, 
     - SSH - Remote for the extension for my VS Code,  
     - Maven For package manager to create a Java Web app from scratch using 
       Java Amazon Correto 8 Version.  

Key concepts I learnt include : 
- How to set up an IAM user for secure AWS access.
- Using VS Code as an IDE and connecting it to your EC2 instance for remote 
   development.
- Installing and utilizing Apache Maven with Amazon Corretto 8 (Java) to manage 
   dependencies and generate a Java web application.
- The foundational steps for preparing a web application for deployment.

### Project reflection

This project took me approximately **3 hours** The most challenging part was ```Remote SSH it was most rewarding to successfully connect my local VS Code directly to my EC2 instance for seamless development.```

Based on my recent experiences, one thing i'm might not have expected in this project is how easily an SSH connection to an EC2 instance could fail after being idle, and the specific steps needed to troubleshoot and reconnect. It highlighted the importance of understanding connection persistence and debugging remote environments.

---

## Launching an EC2 instance

### What I did in this step

In this step, I will launch an EC2 instance on my AWS Console. This EC2 instance will serve as a virtual server in the cloud, providing the compute resources to house and develop my web app's files

I am launching an EC2 instance because it will act as a virtual server in the cloud, providing a home for my web app's files and housing all the development work for this project.


![Image](http://learn.nextwork.org/motivated_teal_shy_hog/uploads/aws-devops-vscode_7852fbf3)

### I also enabled SSH

SSH (Secure Shell) is a protocol that makes sure only authorized users can access a remote server. When I connect to my EC2 instance, SSH verifies my identity using the private key. Once authorized, it sets up a secure, encrypted connection, so all my commands and data are protected.

### Key pairs

A key pair in EC2 is like the keys to my virtual computer. It's an authentication method that lets me securely access your EC2 instance. It consists of two parts: a public key that AWS keeps, and a private key that automatically downloads to my local computer.


### Downloaded key pair file

Once I set up my key pair, AWS automatically downloaded my private key to my local computer. This file is in the *.pem format, which stands for Privacy Enhanced Mail. It's a common file format used to store cryptographic keys for secure remote access to virtual servers like our EC2 instance.

---

## Set up VS Code

### What I did in this step

In this step, I will install VS Code and set up its terminal. This will allow me to create and edit my web app's code, and securely communicate with my EC2 instance. I will also update the permissions of my ```*.pem``` file to ensure a secure connection.


### What is VS Code?

Visual Studio Code (VS Code) is a popular Integrated Development Environment (IDE) developed by Microsoft. It's software that helps me write, edit, and manage code for web and app development. VS Code also includes tools that allow me to connect to and work with virtual servers, such as EC2 instances.


I will use VS Code to connect to my EC2 instance and then create and edit my web app's code. As part of this step, I'll also update the permissions of my ```*.pem``` file to ensure a secure SSH connection to the instance.

![Image](http://learn.nextwork.org/motivated_teal_shy_hog/uploads/aws-devops-vscode_53d05e68)

---

## My first terminal commands

A terminal is Command Line Interface that i give instruction to my computer using text. 

The first command I ran for this project is cd to navigate the terminal path to the destination folder.

### Updating file permissions

I used the ```chmod 400``` command. chmod stands for "_change mode_" and the ```400``` permission setting makes my private key file readable only by me (the owner), restricting access for everyone else. This is a security best practice for private keys.

![Image](http://learn.nextwork.org/motivated_teal_shy_hog/uploads/aws-devops-vscode_9328ada1)

---

## SSH connection to EC2 instance

### What I did in this step

In this step, I will connect to my EC2 instance from VS Code using SSH, because this connection allows me to work directly within the instance to set up the web app.

### Connecting to EC2

To connect to my EC2 instance, I used the command : 
```bash
ssh -i ~/Desktop/DevOps/nextwork-keypair.pem ec2-user@<EC2 instance public dns> 
```
to start a secure shell connection, authenticating with my private key file.

### This command required an IPv4 address

A Public IPv4 DNS is the public address for my EC2 server that the internet uses to find and connect to it. In this project, my local computer will use this IPv4 DNS to connect to my EC2 instance.

![Image](http://learn.nextwork.org/motivated_teal_shy_hog/uploads/aws-devops-vscode_e3069dca)

---

## Maven & Java

### What I did in this step

In this step, I will install Maven and Java Coretto 8 in my instance, I'm doing this because both tools are helpful for setting up a Java web app from scratch

### Why I'm using Maven
![alt text](<assets/mvn package.png>)
Apache Maven is a tool that helps developers build and organize Java software projects. It also acts as a package manager, automatically downloading any external code for project needs.


I'm using Maven in this project because it's a powerful tool for Java web applications. 
1.  Firstly, it acts as a package manager, automatically downloading any external 
    code for project needs. 
2. Secondly, it uses archetypes, which are like project templates, to quickly set up 
    the basic structure for my web app. This helps me get started faster and focus 
    on building the application.


### Why I'm using Java
![alt text](<assets/java version.png>)
Java is a widely used programming language for many applications, from mobile to large enterprise systems. I'm using Amazon Corretto 8, a free and reliable version from Amazon, because Maven needs Java to build our web app in this project.

Java is essential in this project because my web application is built using the Java programming language. I'm need Java installed for Maven to function correctly, as Maven is a build tool that uses Java to compile, manage dependencies, and ultimately generate my web application.

---

## Create the Application

### What I did in this step

In this step, I'm using Maven commands to generate a basic Java web app structure. This helps me quickly set up the project so I can focus on writing code instead of building the project from scratch.

### Creating the Java web app
```bash
 mvn archetype:generate \  ##1st command.  
   -DgroupId=com.nextwork.app \ ## 2nd command. 
   -DartifactId=nextwork-web-project \ ## 3rd command. 
   -DarchetypeArtifactId=maven-archetype-webapp \ ## 4th command. 
   -DinteractiveMode=false ## 5th command
```
1.  ```first command``` to sets up a basic sctructure for a web application, don't need 
    create from scratch.
2. ```Second Command``` to package name for the projects, organize and identify 
    libaries and part of the projects.
3. ```Third Command``` to for project name.
4. ```Fourth Command``` to specifies creating a web application.
5. ```Fifth Command``` to run without user commands confirmation (yes/no)
    and confirmed that it should create a web application without interactive 
    prompts


### Installing Remote - SSH
![alt text](<assets/remote ssh.png>)
I'm installed the Remote - SSH extension in VS Code to connect directly to my EC2 instance via SSH. This allows me to work on files and run programs on the remote server as if they were on my local machine. It's particularly useful for developing on the same operating system as my deployment environment or utilizing more powerful remote hardware, making it much easier to edit and manage my web app.


### SSH configuration details
![alt text](<assets/ssh extension.png>)
Configuration details required to set up a directly SSH remote connection to EC2 instance within include:
1. ```Host``` should match up with the EC2 instance's IPv4 DNS, 
2. ```Hostname``` the actual address of the remote server for connection, 
3. ```Identity File``` fo path to private key rule for authenticating, 
4. ```User``` for username for login

![Image](http://learn.nextwork.org/motivated_teal_shy_hog/uploads/aws-devops-vscode_2939cf01)

---

## Create the Application

### Exploring the project structure

Using VS Code's file explorer, I could see the nextwork-web-project folder, which contains all the files and subfolders of the web app. Specifically, I saw the ```src``` folder, which holds the source code, and the ```pom.xml``` file, which stores Maven configuration details.

The src folder contains all the source code that defines how your web app functions and appears. Within src, the webapp folder holds your web app's front-end files like ```HTML, CSS, JavaScript, and JSP```. Configuration files, such as those for database connections, are typically found in the resources subfolder.

![Image](http://learn.nextwork.org/motivated_teal_shy_hog/uploads/aws-devops-vscode_45f91fd7)

---

## Using Remote - SSH

### What I did in this step

In this step, I am connecting VS Code directly to my EC2 instance. This allows me to use VS Code's full IDE features, such as file navigation and code editing, to manage my web app directly on the instance.

### Updating the web app

The index.jsp is a file in Java web apps that displays web page content, similar to HTML. However, it can also include Java code to create dynamic content that changes, unlike static HTML files.

I edited index.jsp directly on the EC2 instance using VS Code's Remote - SSH extension. This allowed me to modify the files on the virtual server without needing to transfer them to my local computer first.

![Image](http://learn.nextwork.org/motivated_teal_shy_hog/uploads/aws-devops-vscode_7a1de541)
