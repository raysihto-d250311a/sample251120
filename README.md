# sample251120

A test repository for automatically closing pull requests from users without write access.

## Features

This repository automatically closes pull requests from users who do not have write access (collaborators with write, maintain, or admin permissions).

### How it works

- When a pull request is opened or reopened, a GitHub Actions workflow is triggered
- The workflow checks the permission level of the PR author
- If the author does not have write, maintain, or admin access, the PR is automatically closed with a comment

### Workflow

The auto-close functionality is implemented via GitHub Actions workflow located at:
`.github/workflows/auto-close-non-writable-prs.yml`

The workflow:
1. Triggers on `pull_request_target` events (opened, reopened)
2. Checks the PR author's permission level using GitHub API
3. Closes the PR and adds a comment if the author lacks write access