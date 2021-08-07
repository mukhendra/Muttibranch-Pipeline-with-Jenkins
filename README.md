# Muttibranch-Pipeline-with-Jenkins

Pre-Requisites:
Expected a Jenkins server is already up and running
A Git repository with more than one branch
In my case I am using a repository called https://github.com/ravdy/test-nodejs-app.git
Create a Multibranch Pipeline
Login to Jenkins GUI
Click on “New Item” → Specify a job name → Select “Multibranch Pipeline option”

3. Give Display Name and Description
4. Under Branch Sources → Add source → Chose Git → and provide GitHub URL and Credentials (Credentials are optional if it is public repo)

Branch Source Image

Git Repo Information
5. Under Build Configuration → chose Jenkinsfile path. Most of the case it will be under Repo root directory.

Jenkinsfile path
6. Apply and Save the job
Now Jenkins automatically scans the repository and create a job for each branch wherever it finds a Jenkinsfile and initiate first build.

Multibranch Pipeline
Using Webhook
If you wish to automate the build process in the multibranch pipeline we can use Webhook. This feature is not enabled until we install “Multibranch Scan Webhook Trigger”. This enables an option “scan by webhook” under “Scan Multibranch Pipeline Triggers”. Here we should give a token. I am giving it as “mytoken”. by this time your job looks something like below.

Jenkins Multibranch pipeline with webhook
Now to enable auto build process we should provide Jenkins URL with token in the GitHub. in this case like should be http://65.0.130.108:8080/multibranch-webhook-trigger/invoke?token=mytoke
for this log into GitHub → settings → Webhooks → Add webhook

Provide Payload URL as “http://65.0.130.108:8080/multibranch-webhook-trigger/invoke?token=mytoke” and Content type as “application/json” and click on Add webhook

Once this is done you can see a new webhook and its time to do some changes in the repository to test the webhook connection.

In this demonstration, I am going to create a new branch called “stage” and push the changes onto remote repo.

New branch creation on Git and pushed changes onto GitHub
Now you could see a build has been triggered automatically on Jenkins and it scan and create a job for the new branch as well.


For Reference :

https://valaxytech.medium.com/?p=a65decede4f8
https://dzone.com/articles/implement-ci-for-multibranch-pipeline-in-jenkins

https://devopscube.com/jenkins-multibranch-pipeline-tutorial/
