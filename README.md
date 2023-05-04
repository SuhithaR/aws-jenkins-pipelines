# Integrating Jenkins with AWS CodeBuild and AWS CodeDeploy to create a CI/CD pipeline
A working CI/CD pipeline is produced by deploying AWS CodeBuild artefacts with AWS CodeDeploy using the open-source Jenkins automation server. The CI/CD pipeline is triggered by code changes committed to your GitHub repository, automatically fed into CodeBuild, and the output is deployed to CodeDeploy when fully implemented.

Your source code is compiled by a fully controlled build service that is created by a working pipeline. After that, it creates code artefacts that CodeDeploy may utilise to automatically deploy to your production environment.

![image](https://user-images.githubusercontent.com/91371224/236111285-ff908fbb-ea08-4957-af29-bd97d5c718a5.png)

# Overview
assembling the necessary resources, such as the Jenkins server, the CodeBuild project, and the CodeDeploy application.

unlocking and gaining access to the Jenkins server.

establishing a project and setting up the Jenkins plugin for CodeDeploy.

testing every step of the CI/CD process.

# Create the resources
How to start an AWS CloudFormation template, a programme that generates the subsequent resources:

The files from the GitHub repository and the CodeBuild artefact application file that CodeDeploy utilises are kept in an Amazon S3 bucket. The Jenkins server is given access to the S3 bucket by the IAM S3 bucket policy. Using an Amazon EC2 instance as a Jenkins server requires the JenkinsRole IAM role and instance profile. With the help of this role, Jenkins running on the EC2 instance is able to write files to the S3 bucket and create CodeDeploy deployments. Application and deployment group for CodeDeploy. An IAM role that allows CodeDeploy to access the tags applied to the instances or the names of the EC2 Auto Scaling groups connected to the instances is the CodeDeploy service role. An IAM role and instance profile for the EC2 instances of CodeDeploy.

![image](https://user-images.githubusercontent.com/91371224/236111495-c742dd8b-8bf3-4911-bb3c-26771dd64b71.png)

![image](https://user-images.githubusercontent.com/91371224/236111518-3beabed5-cbf6-4cee-8820-485b33cc53fc.png)

# Unlock and gain access to your Jenkins server.
From the CloudFormation stack's Outputs tab, copy the JenkinsServerDNSName value, and then paste it into your browser.

Use the IP address and key combination from Unlocking Jenkins to SSH to the server and follow the on-screen steps to unlock the Jenkins server.

To copy the automatically created alphanumeric password (between the two sets of asterisks), Cat the log file at /var/log/jenkins/jenkins.log as the root user. Then, as seen in the following screenshots, use the password to unlock your Jenkins server.

![image](https://user-images.githubusercontent.com/91371224/236111581-9b54acfc-f81b-4604-8e5b-a4979271de8a.png)

![image](https://user-images.githubusercontent.com/91371224/236111601-fe88a6f1-8034-478c-8458-11efea3628c3.png)

![image](https://user-images.githubusercontent.com/91371224/236111610-78781c5d-62c9-4bad-a223-c2212262f0af.png)

![image](https://user-images.githubusercontent.com/91371224/236111623-386aa461-134c-46ed-9115-be9599cfa421.png)

# The entire CI/CD process is tested.
Create an application and upload it to your GitHub repository to test the entire solution.

An application tree including the application's source files, including text and binary files, executables, and packages, can be seen in the following screenshot:

![image](https://user-images.githubusercontent.com/91371224/236111689-69ad3818-846d-48aa-8865-c11eceff05c7.png)

The templates directory, test_app.py, and web.py are the application files in this example.

The primary application specification file that instructs CodeDeploy how to deploy your application is called appspec.yml. Jenkins manages each deployment as a set of defined lifecycle event "hooks" using the AppSpec file. AWS CodeDeploy AppSpec File Reference contains instructions on how to generate an AppSpec file that is correctly formatted.

CodeBuild uses the buildspec.yml file, which is a collection of build instructions and associated settings, to do builds. A build spec can be defined when you start a build project or it can be included as part of the source code. How AWS CodeBuild Works has further details.

According to the needs of your application, the scripts folder contains the scripts that you would like to execute during the CodeDeploy LifecycleHooks execution. Plan a Revision for AWS CodeDeploy for further details.

Follow these steps to test this solution:

Run the following git commands from the path where your sample application is located to unzip the application files and upload them to your GitHub repository:

$ git add -A 

$ git commit -m 'Your first application'

$ git push Wait two minutes for the previously defined project trigger on the Jenkins server dashboard to begin functioning. You need to see a new build occurring as soon as the trigger gets going.

Examine the build events and the actions taken by each Jenkins plugin on the Jenkins server Console Output page. You can examine the CodeDeploy deployment in more depth, as demonstrated in the screenshot below:

![image](https://user-images.githubusercontent.com/91371224/236111887-9607cbdb-8c6c-439a-a089-7cbcd0646433.png)

Jenkins ought to confirm that you've successfully deployed a web application after it's finished. In order to verify that the deployed application is functioning properly, you can also utilise your ELBDNSName value.

![image](https://user-images.githubusercontent.com/91371224/236111915-3be7682a-241c-4b3d-9d9f-217795a31a6b.png)










