# Day 42: IAM Programmatic Access and AWS CLI 🚀☁  

Today is more of a reading exercise and getting some programmatic access for your AWS account.  

## IAM Programmatic Access  

In order to access your AWS account from a terminal or system, you can use AWS Access keys and AWS Secret Access keys.  
Watch [this video](https://youtu.be/XYKqL5GFI-I) for more details.  

### Steps for IAM Programmatic Access  

1. Log in to your **AWS Management Console**.  
2. Navigate to the **IAM (Identity and Access Management)** service.  
3. Go to the **Users** section and:  
   - Select an existing user, or  
   - Create a new user by clicking the **Add users** button.  
4. Under **Access Type**, select **Programmatic Access**.  
5. Assign permissions to the user:  
   - Attach an appropriate policy (e.g., `AdministratorAccess` for full access or a custom policy for limited access).  
6. Review and create the user.  
7. Once created, download the **Access Key ID** and **Secret Access Key**.  
   - These keys are required to configure AWS CLI.  

## AWS CLI  

The AWS Command Line Interface (AWS CLI) is a unified tool to manage your AWS services. With just one tool to download and configure, you can control multiple AWS services from the command line and automate them through scripts.  

### Key Features of AWS CLI v2:  
- Improved installers  
- New configuration options (e.g., AWS IAM Identity Center)  
- Interactive features  

### Steps to Install and Configure AWS CLI:  

1. Download and install AWS CLI:  
   - **Windows**: [Installation Guide](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).  
   - **macOS**: Use Homebrew:  
     ```bash
     brew install awscli
     ```  
   - **Linux**: Follow the [Linux installation steps](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).  

2. Verify the installation:  
   ```bash
   aws --version
