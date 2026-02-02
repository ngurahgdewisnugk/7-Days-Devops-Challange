<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Connect a GitHub Repo with AWS

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-github)

**Author:** Ngurah Gede Wisnu Gudakesa  
**Email:** ngurahgedewisnugk@gmail.com

---

## Connect a GitHub Repo with AWS

![Image](http://learn.nextwork.org/motivated_teal_shy_hog/uploads/aws-devops-github_dd9d254e)

---

## Introducing Today's Project!

In this project, I will set up a ```Git``` repository on ```GitHub``` to safely store my web application's code in the development instance cloud. I'm doing this to understand the workflow process from a development environment to version control system, which is a crucial step for building CI/CD pipelines and enabling efficient code handoffs.

### Key tools and concepts

*   **Development Environment:** EC2 Instance used as the primary workspace.
*   **Version Control:** Git for local repository management and GitHub for cloud-based remote storage.
*   **Workflow Mastery:** Configured Git on EC2 and connected the local project to a GitHub repository.
*   **Synchronization:** Learned the process of staging, committing, and pushing changes to synchronize local code with the cloud.
*   **Documentation:** Established a `README.md` file to provide a professional introduction and project overview.

### Project reflection

*   **Duration:** Approximately 3 hours.
*   [**Challenge:**](<### Challange: Resolving 403 Permission Denied Error>) Setting up the GitHub Personal Access Token (PAT) and troubleshooting authentication issues.
*   **Reward:** Successfully establishing a secure connection between the local EC2 repository and GitHub.
*   **Goal:** This project is part of a DevOps series aimed at mastering CI/CD pipelines to accelerate my career in cloud-native orchestration.

---

## Git and GitHub

Git is like a time machine and filing system for your code. It tracks every specific change you make and when they were made. This allows you to easily go back to an earlier version of your work if something breaks, and it also makes teamwork and collaboration much easier by showing who made specific changes. It's often referred to as a version control system.

I installed Git on my EC2 instance using the following commands:
*   `sudo dnf update -y`: Updates all existing software on the instance to the latest versions.
*   `sudo dnf install git -y`: Installs the Git software package.

GitHub is a storage space for different version of my project that Git tracks, I'm using GitHub in this project to see my projects in a more user-friendly way and useful in situation with what and where I'm working with. 

![Image](http://learn.nextwork.org/motivated_teal_shy_hog/uploads/aws-devops-github_efaadbf7)

---

## My local repository
![alt text](<Assets/local repository.png>)

A Git repository (or "repo") is like a special folder that holds all my project's code and files, along with it's complete version history. It tracks every change I made, allowing me to manage and collaborate on my code effectively.

*   **Initialization:** The `git init` command sets up a new local repository in the current directory.
*   **Branching:** A branch is a parallel timeline for code. By default, `git init` creates a branch typically named `main` or `master`.


![Image](http://learn.nextwork.org/motivated_teal_shy_hog/uploads/aws-devops-github_7bf21bae)

---

## To push local changes to GitHub, I ran three commands

### git add

The first command was ```git add .``` .This command stages all files in your current project directory, preparing them to be included in the next version of your project's history. The staging area acts as a temporary holding space where you can review all your modified files before you officially save them with a commit.

### git commit

The second command I ran was ```git commit -m "<message for updated version>"```: 
- This command saves the changes I have prepared into my project's version history as a new snapshot. 
- Using `-m` means I leaving a message describing what the `commit` is about, which helps me and others understand what changes were made in this version.

### git push

The third command I ran was ```git push -u origin main```: 
- This command uploads my committed changes to `origin`, which is my bookmarked GitHub repository. 
- The `main` part tells Git to push these updates to the master branch on my GitHub repo. 
- Using `-u` sets an upstream for my local branch, so Git remembers to push to master by default, allowing me to simply run git push next time.

---

### Challange: Resolving 403 Permission Denied Error 

When attempting to push to the GitHub repository, I encountered a 403 error:
```bash
remote: Permission to ngurahgdewisnugk/nextwork-web-project.git denied to xxxxxxx. fatal: unable to access 'https://github.com/ngurahgdewisnugk/nextwork-web-project.git/': The requested URL returned error: 403
```
This error indicates an authentication issue where Git was using cached credentials from a different GitHub account (xxxxxxx) instead of the correct account (ngurahgdewisnugk).

#### Root Cause

The 403 error occurs when:
- Git has cached credentials for a different user.
- The credential helper is storing outdated authentication information.
- The remote URL doesn't explicitly specify the correct username

#### The Solution
To resolve this authentication conflict, I cleared the cached credentials and updated the remote URL:
```bash
# Step 1: Clear global credential cache
git config --global --unset credential.helper

# Step 2: Clear local credential cache
git config --local --unset credential.helper

# Step 3: Update remote URL with explicit username
git remote set-url origin https://<github_username>@github.com/<github_username>/<repository_name>.git
```

#### Applied to My Repository 
![alt text](<Assets/success push.png>)
---

## Authentication

When pushing changes to GitHub, Git asks for my credentials to authenticate my identity and ensure that I have permission to push changes to the connected remote repository.


### Local Git identity

Git needs my name and email to track who made each change in the project's history. This ensures that every commit is associated with the correct author.


Running git log showed me a detailed history of all commits, including the author's name and email, the commit message, and the unique commit ID. This allows me to track every change made to the project and easily identify who made those changes.


![Image](http://learn.nextwork.org/motivated_teal_shy_hog/uploads/aws-devops-github_9a27ee3b)

---

## GitHub tokens

GitHub authentication failed when I entered my password because GitHub no longer accepts passwords for Git operations over HTTPS due to security risks. Instead, a Personal Access Token (PAT) is required for authentication.


A GitHub token is a key authentication long string with a random letter, I'm using one in this project because GitHub has stopped supporting password authentication for connecting to repositories over HTTPS due to security risks. Using a Personal Access Token (PAT) is a much more secure way to authenticate and interact with your repositories, as tokens are unique and very difficult to guess.

I set up a GitHub token by navigating to the Developer settings in my GitHub account settings. From there, I selected Personal access tokens, then Tokens (classic), and chose to Generate new token (classic). 

![alt text](<Assets/developer settings.png>)

I provided a descriptive note for easy identification and set an expiration limit. Crucially, I also selected the repo scope to grant the necessary permissions. 

Finally, I clicked Generate token and immediately copied the new token to a safe place.

![Image](http://learn.nextwork.org/motivated_teal_shy_hog/uploads/aws-devops-github_fa11169d)

---

## Making changes again

I updated the `index.jsp` file.

To make my changes visible in my GitHub repository : 
1.  I first added the modified `index.jsp` file to the staging area using git add . 
2. After verifying the changes with `git diff --staged`, 
3. I committed them with a message using `git commit -m "message"`. 
4. Finally, I pushed these committed changes from my local repository to my GitHub repository in the cloud using git push.

![Image](http://learn.nextwork.org/motivated_teal_shy_hog/uploads/aws-devops-github_6becb2bc)

---

## Setting up a README file

A README file is a document, usually written in Markdown, that serves as the introduction to your project in a GitHub repository. Its main purpose is to explain what your project is about, how to set it up, and how to use it. It's often the first thing people see when they visit your repository, providing essential information at a glance.

[My README]() file has sections that outline Project Titile, Table of Contents, Introduction, Technologies , Setup, Contact, Conclusion

![Image](http://learn.nextwork.org/motivated_teal_shy_hog/uploads/aws-devops-github_c94976902)

---
