
# GitHub Actions SQLite Encryption Example

This project demonstrates how to use GitHub Actions with secrets to securely access an encrypted SQLite database using SQLCipher.

## Setup Instructions

### Step 1: Fork the Repository

First, fork this repository to your GitHub account:

1. Click the "Fork" button at the top-right corner of this repository page.
2. Select your GitHub account as the destination for the fork.

### Step 2: Set Up the Secret in GitHub

You need to add a secret to your forked GitHub repository to store the database password. The name of the secret can be found in the provided GitHub Actions workflow file.

1. Go to your forked GitHub repository.
2. Click on `Settings`.
3. Click on `Secrets and variables` in the left sidebar.
4. Click on `Actions`.
5. Click on `New repository secret`.
6. Use the appropriate name for the secret as specified in the GitHub Actions workflow file and set its value to the password for the provided database, which is `question_password`.
7. Click the `Add secret` button.

### Step 3: Configure GitHub Actions Workflow

The GitHub Actions workflow is configured to use the secret to access the encrypted SQLite database. Here's the workflow file `.github/workflows/test-db.yml`:

```yaml
name: SQLite DB Test

on: 
  push:
    branches: [main]
  workflow_dispatch:

jobs:
  db-test:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Install SQLCipher
      run: sudo apt-get install -y sqlcipher

    - name: Test SQLite Database
      run: |
        sqlcipher github_actions_question.db -cmd "PRAGMA key = '${{ secrets.DB_PASSWORD }}'; SELECT value FROM answer;"
```

This workflow will:
1. Checkout the repository.
2. Install SQLCipher.
3. Open the encrypted database using the secret and select the value from the `answer` table.

### Step 4: Verify the Workflow

You can manually trigger the workflow from the GitHub Actions interface:

1. Go to the `Actions` tab in your GitHub repository.
2. Select the `SQLite DB Test` workflow.
3. Click the `Run workflow` button.

Check the Actions tab in your GitHub repository to see the workflow run and verify that it completes successfully and displays the contents of the `answer` table.

### Step 5: Show Proof

Provide the value from the `answer` table as proof of your workflow setup.

---

By following these instructions, you will have set up a GitHub Actions workflow that securely accesses an encrypted SQLite database using a secret stored in the repository settings and displays the contents of the `answer` table.
