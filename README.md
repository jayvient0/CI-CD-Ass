Assignment CI/CD

1. Project Overview
• Website: Static HTML
• Version Control: GitHub.
• CI/CD Tool: GitHub Actions.
• Cloud Provider: AWS (S3 Bucket).

2. CI/CD Pipeline Architecture
The deployment process follows a fully automated workflow. Upon every push to the main branch, a GitHub Action runner is initialized to synchronize the repository with the production environment.
Key Components of the YAML Configuration:
• Automated Trigger: Configured to run only on the main branch to ensure stability.
• Security: Leveraged GitHub Actions Secrets to store AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY, ensuring no sensitive credentials reside in the source code.
• Efficiency: Used the aws s3 sync command with the --delete flag. This ensures the S3 bucket is a mirror of the repository, automatically removing old files.
• Clean Deployment: Implemented --exclude rules to prevent development metadata (like .git/ or .github/) from being uploaded to the public web server.

3. Integration & Deployment Process
To bridge the gap between GitHub and AWS, I configured an IAM (Identity and Access Management) user with the AmazonS3FullAccess policy. This provides the "Principle of Least Privilege" required for the automation runner to manage the S3 bucket objects.
Verification Steps:
1. Code Update: Modified index.html locally.
2. Git Push: Pushed changes to GitHub.
3. Pipeline Execution: Monitored the Actions tab to verify a successful "Exit Code 0" status.
4. Live Check: Verified the changes were live on the AWS S3 Static Website Endpoint.

   
4. Evaluation Checklist Summary
• Quality & Structure: Pipeline uses standardized GitHub Actions (v4) and secure secret management.
• Clear Demonstration: Full history of successful deployments is available in the GitHub Actions logs.
• Proper Integration: Seamless handshake between GitHub runners and AWS S3 via the AWS CLI.
