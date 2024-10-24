# Lab: Integrating GitHub Repo with Jenkins Freestyle Project

## Objective
In this lab, you will learn how to integrate a GitHub repository into a Jenkins Freestyle Project and trigger the build automatically when there are changes to the GitHub repository.

## Prerequisites
- Jenkins installed and running.
- GitHub repository with proper access.
- Git plugin installed in Jenkins.
- Webhook permission for the GitHub repository.
  
### Step 1: Configure Jenkins with GitHub Repository

1. **Create a New Freestyle Project**
   - Log in to Jenkins.
   - Click on `New Item`.
   - Enter a name for your project, select `Freestyle project`, and click `OK`.

2. **Configure GitHub Repository**
   - In the project configuration, scroll down to the **Source Code Management** section.
   - Select `Git`.
   - In the `Repository URL` field, enter the URL of your GitHub repository (e.g., `https://github.com/<username>/<repo-name>.git`).
   - If the repository is private, click on `Add` next to **Credentials** and enter your GitHub username and Personal Access Token (PAT).

3. **Branch to Build**
   - Specify the branch to build, usually `main` or `master`:
     - In **Branch Specifier**, enter `*/main` (replace `main` with the branch name you want to track).

### Step 2: Enable Build Trigger for GitHub Webhook

1. **Set Build Triggers**
   - Scroll down to the **Build Triggers** section.
   - Check the option `GitHub hook trigger for GITScm polling`.
   - This allows the Jenkins job to be triggered automatically when a change is pushed to the GitHub repository.

### Step 3: Configure GitHub Webhook

1. **Go to GitHub Repository**
   - Navigate to the GitHub repository you want to integrate with Jenkins.

2. **Add Jenkins Webhook**
   - Go to `Settings` > `Webhooks`.
   - Click on `Add webhook`.
   - In the **Payload URL** field, enter the URL of your Jenkins server followed by `/github-webhook/` (e.g., `http://<jenkins-server>/github-webhook/`).
   - Set the **Content type** to `application/json`.
   - Choose `Just the push event` or select specific events to trigger the job.
   - Click on `Add webhook`.

### Step 4: Add Build Steps in Jenkins

1. **Add a Build Step**
   - In your Jenkins project configuration, scroll down to the **Build** section.
   - Click `Add build step`, then select `Execute shell` (or any other action based on your project needs).
   - Enter the shell commands or scripts to be executed during the build. For example:
     ```bash
     echo "Building the project..."
     ```

### Step 5: Save and Build the Project

1. **Save the Project Configuration**
   - Click on `Save` to save your project settings.

2. **Trigger a Manual Build (Optional)**
   - Click `Build Now` on the left side of the project page to verify that the configuration is working.
   
3. **Automatic Build Trigger**
   - Push changes to the GitHub repository.
   - After pushing changes, Jenkins should trigger the build automatically due to the webhook.

### Step 6: Verify Build

1. **Check Build Status**
   - Go to the Jenkins project page and click on `Build History` to see the status of your triggered builds.
   - You should see a new build triggered by the webhook when you pushed to the GitHub repository.

---
