# sample251120

A test repository for automatically closing pull requests from users without write access.

## Features

This repository automatically closes pull requests from users who do not have write access (collaborators with write, maintain, or admin permissions).

### How it works

- When a pull request is opened or reopened, a GitHub Actions workflow is triggered
- The workflow checks the permission level of the PR author
- If the author does not have write, maintain, or admin access, the PR is automatically closed with a comment
- Comments are posted by the "auto-close-agent" GitHub App

### Workflow

The auto-close functionality is implemented via GitHub Actions workflow located at:
`.github/workflows/auto-close-non-writable-prs.yml`

The workflow:
1. Triggers on `pull_request_target` events (opened, reopened)
2. Generates an authentication token from the GitHub App
3. Checks the PR author's permission level using GitHub API
4. Closes the PR and adds a comment if the author lacks write access

## Setup

To use this workflow, you need to set up a GitHub App named "auto-close-agent":

### 1. Create a GitHub App

1. Go to your organization or user settings
2. Navigate to "Developer settings" > "GitHub Apps" > "New GitHub App"
3. Configure the app:
   - **Name**: `auto-close-agent`
   - **Homepage URL**: Your repository URL
   - **Webhook**: Uncheck "Active"
   - **Permissions**:
     - Repository permissions:
       - Pull requests: Read & write
       - Metadata: Read-only
   - **Where can this GitHub App be installed?**: Only on this account
4. Create the app and note the **App ID**
5. Generate and download a **private key**

### 2. Install the GitHub App

1. Go to the app settings
2. Click "Install App"
3. Select the repository where you want to use it
4. Complete the installation

### 3. Configure Repository Secrets

Add the following secrets to your repository:

1. Go to repository Settings > Secrets and variables > Actions
2. Add the following secrets:
   - `AUTO_CLOSE_APP_ID`: The App ID from step 1
   - `AUTO_CLOSE_PRIVATE_KEY`: The private key content from step 1

### 4. Verify

Once configured, the workflow will automatically run when PRs are opened or reopened, and comments will appear from the "auto-close-agent" app.