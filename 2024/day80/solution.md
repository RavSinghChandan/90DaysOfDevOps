# Automating CI/CD with Jenkins and GitHub

## Project Description
This guide will help you automate the build, test, and deployment process of a web application using Jenkins and GitHub. You'll set up seamless integration with GitHub webhooks to trigger Jenkins pipelines upon changes.

---

## Steps to Implement

### 1️⃣ Prerequisites

1. **Install Jenkins**
   - Ensure Java is installed: `java -version`
   - Download Jenkins: [Jenkins Official Site](https://www.jenkins.io/)
   - Install and start Jenkins: `sudo apt install jenkins` (Linux) or use the installer for your OS.

2. **Set Up GitHub Repository**
   - Create a GitHub repository for your project.
   - Push your web application code to the repository.

3. **Install Git on Jenkins Server**
   - Install Git: `sudo apt install git`
   - Configure Git: `git config --global user.name "Your Name"` and `git config --global user.email "you@example.com"`.

---

### 2️⃣ Setting Up Jenkins with GitHub

1. **Install Jenkins Plugins**
   - Navigate to `Manage Jenkins` > `Manage Plugins`.
   - Install the following plugins:
     - Git Plugin
     - GitHub Integration Plugin
     - Pipeline Plugin

2. **Generate GitHub Token**
   - Go to your GitHub account settings > Developer Settings > Personal Access Tokens.
   - Generate a new token with `repo` and `admin:repo_hook` permissions.

3. **Configure Jenkins with GitHub**
   - In Jenkins, go to `Manage Jenkins` > `Manage Credentials` > `Global Credentials`.
   - Add a new credential:
     - Kind: Secret Text
     - Secret: Your GitHub Token
     - ID: `github-token`

---

### 3️⃣ Create the CI/CD Pipeline

1. **Set Up a New Job**
   - In Jenkins, create a new item > Select `Pipeline` > Name your job.
   - Under `Pipeline` > `Definition`, select `Pipeline Script from SCM`.
   - Add your repository URL and branch.

2. **Write the Jenkinsfile**
   Create a `Jenkinsfile` in your GitHub repository with the following content:

   ```groovy
   pipeline {
       agent any

       stages {
           stage('Build') {
               steps {
                   echo 'Building the application...'
                   sh 'npm install' // or your build command
               }
           }

           stage('Test') {
               steps {
                   echo 'Running tests...'
                   sh 'npm test' // or your test command
               }
           }

           stage('Deploy') {
               steps {
                   echo 'Deploying the application...'
                   sh './deploy.sh' // your deployment script
               }
           }
       }

       post {
           failure {
               echo 'Pipeline failed!'
               // Add email or Slack notifications here if required
           }
       }
   }
   ```

---

### 4️⃣ Configure Webhooks

1. **Add a Webhook in GitHub**
   - Go to your GitHub repository > Settings > Webhooks > Add Webhook.
   - Payload URL: `http://<Jenkins-Server-IP>:8080/github-webhook/`.
   - Content Type: `application/json`.
   - Select events: `Just the push event`.

2. **Test the Webhook**
   - Push a change to your repository to trigger the webhook.

---

### 5️⃣ Monitor and Manage the Pipeline

1. **View Pipeline in Jenkins**
   - Go to the Jenkins job dashboard.
   - Check the console output for each build to debug or monitor progress.

2. **Notifications**
   - Configure email notifications: `Manage Jenkins` > `Configure System` > Email Notification.
   - Use plugins for Slack or other tools for prompt alerts.

---

### 🎯 Benefits

- Automates workflows and reduces manual errors.
- Ensures quick feedback through testing.
- Simplifies deployments for consistent environments.

Start building your CI/CD pipeline and streamline your development workflow today!
