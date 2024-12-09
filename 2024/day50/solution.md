# Day 50: Your CI/CD Pipeline on AWS - Part 1 🚀☁  

In this guide, you’ll learn how to set up a source control repository with AWS CodeCommit as the foundation of your CI/CD pipeline.  

## Tools We’ll Use  
- **AWS CodeCommit**  
- **Git**  

---

## Step 1: Setting Up CodeCommit Repository  
1. **Create a Repository in AWS CodeCommit**  
   - Log in to your AWS Management Console.  
   - Navigate to **CodeCommit** under the **Developer Tools** section.  
   - Click **Create Repository**.  
   - Provide a name and optional description for your repository, then click **Create**.  

2. **Set Up IAM Permissions**  
   - Go to **IAM** in AWS Management Console.  
   - Create or modify a user with the **CodeCommitFullAccess** policy.  

3. **Generate Git Credentials**  
   - In the IAM Console, select your user.  
   - Go to the **Security credentials** tab.  
   - Click **Generate Git credentials for AWS CodeCommit** and download the credentials.  

---

## Step 2: Cloning the Repository Locally  
1. Install **Git** if you don’t already have it on your machine.  
   - On macOS:  
     ```bash
     brew install git
     ```  
   - On Ubuntu:  
     ```bash
     sudo apt update && sudo apt install git
     ```  

2. Clone the Repository:  
   - Open your terminal and run:  
     ```bash
     git clone https://git-codecommit.<region>.amazonaws.com/v1/repos/<repository-name>
     ```  
   - Replace `<region>` with your AWS region and `<repository-name>` with your repository name.  

3. Change into the repository directory:  
   ```bash
   cd <repository-name>
