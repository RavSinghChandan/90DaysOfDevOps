# Day 51: Mastering CI/CD on AWS - Part 2 🚀☁️  

The journey to building a robust CI/CD pipeline on AWS continues! Today, we'll focus on **AWS CodeBuild**, the next essential tool in the pipeline.

---

## 🛠️ Tasks for Today

### Task 1: Learn About Buildspec Files  
1. Understand what a `buildspec.yaml` file is and its role in defining build commands for CodeBuild.  
2. Explore its structure and common configurations:
   - **phases**: Install, Pre-build, Build, Post-build.
   - **artifacts**: Define output files for deployment.

### Task 2: Build an HTML Page with Nginx  
1. **Create an HTML File**:  
   - Add a simple `index.html` file in your CodeCommit repository.  
   - Example:
     ```html
     <!DOCTYPE html>
     <html>
     <head>
       <title>Welcome to CI/CD with AWS</title>
     </head>
     <body>
       <h1>Hello from AWS CodeBuild!</h1>
     </body>
     </html>
     ```
2. **Set Up Nginx**: Use AWS CodeBuild to automate deployment using Nginx.

### Task 3: Complete the Build Process  
1. Add a `buildspec.yaml` file to your CodeCommit repository with configurations for building and deploying the HTML file.  
   - Example:
     ```yaml
     version: 0.2
     phases:
       build:
         commands:
           - echo Building HTML file...
           - cp index.html /usr/share/nginx/html
     artifacts:
       files:
         - index.html
     ```
2. Run the build process in CodeBuild and ensure it completes successfully.

---

## 📚 Learn More  
Watch this [video tutorial](https://youtu.be/p5i3cMCQ760) for step-by-step guidance.

---

## 🚀 What's Next?  
In the next sessions, we'll explore:
- **CodePipeline**
- **CodeDeploy**
- **S3**  
Stay tuned for more learning opportunities!

---

**Happy Learning! 😊**
