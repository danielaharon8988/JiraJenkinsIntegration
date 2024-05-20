**the task - Jenkins and Git Integration:** 
1. Deploy the following services:
   a. Jira server
   b. Jenkins server
Use your chosen configuration and infrastructure as code utility (Terraform/Chef/Kubernetes/Docker compose/ ... ) I chose to use docker compose
2. Connect Jenkins to a Git repository
3. Create a Job in Jenkins, and a pipeline that will:
   a. when a git branch is merged into master branch:
   b. Extract the Jira issue key from the branch name (Issue key is of the form: EX-123, means string of capital letters, followed by a
   hyphen, followed by an integer)
   c. Move the Jira issue to “Done”

### So, lets solve it: 
![image](https://github.com/danielaharon8988/JiraJenkinsIntegration/assets/157954544/cf0a33af-b4c6-4c92-954e-d1d9decf4c79)
