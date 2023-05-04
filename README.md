# Integrating Jenkins with AWS CodeBuild and AWS CodeDeploy to create a CI/CD pipeline
A working CI/CD pipeline is produced by deploying AWS CodeBuild artefacts with AWS CodeDeploy using the open-source Jenkins automation server. The CI/CD pipeline is triggered by code changes committed to your GitHub repository, automatically fed into CodeBuild, and the output is deployed to CodeDeploy when fully implemented.

Your source code is compiled by a fully controlled build service that is created by a working pipeline. After that, it creates code artefacts that CodeDeploy may utilise to automatically deploy to your production environment.

![image](https://user-images.githubusercontent.com/91371224/236111285-ff908fbb-ea08-4957-af29-bd97d5c718a5.png)
