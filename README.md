# Setting Up WebPage with AWS / GitHub / CI/CD (Jenkins) / AWS DEPLOY

## Summary 
The workflow to setup an webpage using all above listed tool and Deploy them on Ec2 Instance with AutoScalling and Loadbalancer

## Workflow Description: 
- It should deploy a simple web application to a server on a code push to a repository.
- The deployed web application should be reachable on any web browser.
- Make it scalable such that when load increases the number of servers scale up and down making
- sure the new servers have the updated code.

**GitHub Repository**
- The GitHub Repository consist of code of web project where I have added Dockerfile  for the CI/Cd configurations setup pipeline. 

**CI/CD Pipeline** : Createing Pipeline jobs :  
- Job Name: This Jenkins pipeline automates the process of building and uploading a Java application to AWS S3.

**Agent and Environment:**
- The pipeline can run on any available agent.
- Sets the default AWS region to ap-south-1.

**Stages:**

- git-clone: Clones the repository student-ui from GitHub.
- Build: Runs the Maven build command (mvn clean package) to compile and package the Java application.
- aws-cli-installation: Installs or updates the AWS CLI by downloading, unzipping, and installing it.
= add-credentials: Uses AWS credentials (from aws-cred) to verify access by listing S3 buckets with the aws s3 ls command.
- upload-to-s3: Uploads the built .war file to an S3 bucket (oriservetask1).


## AWS-Cloud 

**IAM**
- IAM role created with S3FullAccess, CodeDeployFullAccess, and AutoScaling permissions for seamless AWS web application deployment. This role ensures proper access to S3 for storage, CodeDeploy for application updates, and AutoScaling for efficient resource management.

**S3- Storage** 
- I created an S3 bucket named task-student-ui in AWS to store deployment artifacts. The bucket has full S3 access permissions, managed through an AWS IAM role with AmazonS3FullAccess, allowing Jenkins to interact with the bucket for upload and download operations.
- In the Jenkins pipeline, the upload-to-s3 stage was introduced to automatically upload a .war file to the S3 bucket after the build process. The stage uses AWS credentials (aws-cred) stored in Jenkins to run the AWS CLI command:
### aws s3 cp /var/lib/jenkins/workspace/Task-1/target/studentapp-2.2-SNAPSHOT.war s3://task-student-ui

**AWS CodeDeploy Setup**

-In this project, I set up AWS CodeDeploy to automate the deployment process. Here's a brief overview:
-Created an application with the Compute Platform set to EC2/On-premises.
-Configured a deployment group with the service role ARN arn:aws:iam::025066249552:role/Oriserve_task_CodeDeploy and selected the deployment configuration.
-Set up deployment to use an Amazon S3 bucket for storing application revisions, with deployment overrides set to apply changes all at once.

**Deployment Process:**

- Artifact Retrieval: CodeDeploy retrieves the application artifact from the specified S3 bucket.
- Deployment Execution: CodeDeploy deploys the artifact to the target EC2 instances or on-premises servers. It follows the deployment configuration settings (e.g., deploying all at once, or in phases).

  ## Problem Statement

- I worked on a project involving cloning and redeploying files. I created a shell script to automate the creation of test.txt files in all oriserve directories within the projects directory. The script identifies oriserve folders and places a test.txt file in each, as demonstrated by the updated directory structure. Additionally, I uploaded files including WebContent, src, README.md, dockerfile, pom.xml, and settings.xml.








 
