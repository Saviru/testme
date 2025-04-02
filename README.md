# Automatic Repository Sync Bot 🔄

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat&logo=githubactions&logoColor=white)](https://github.com/features/actions)
[![Sync Repositories](https://github.com/Saviru/Automatic_repo-sync-bot/actions/workflows/repo-sync-bot.yml/badge.svg)](https://github.com/Saviru/Automatic_repo-sync-bot/actions/workflows/repo-sync-bot.yml)

A powerful GitHub Action workflow that automatically synchronizes repositories, allowing you to maintain mirrors or backups of your code with flexible branch mapping. **You can direcly use this as a template and create your project without any other work or copy and pasting.**

<br>

## 🌟 Features

- **Automatic Syncing**: Synchronize repositories on every push or manually trigger syncs
- **Smart Branch Mapping**: Configurable branch mapping with intelligent defaults
- **Status Tracking**: Generates detailed sync status reports
- **Flexible Configuration**: Use environment variables or repository secrets
- **Secure**: Uses token-based authentication for secure operations

<br>

## 📋 Setup Instructions

### 1. Create the Workflow File

Create a file at `.github/workflows/repo-sync-bot.yml` in your source repository and copy the workflow provided in this repository.

### 2. Configure Authentication

You need a Personal Access Token (PAT) with appropriate permissions:

1. Go to your GitHub account → Settings → Developer settings → Personal access tokens → Fine-grained tokens (or Classic tokens)
2. Create a new token with the following permissions:
   - `repo` scope for private repositories
   - `public_repo` scope for public repositories
   - Add `workflow` scope if you want to sync workflow files
3. Copy the token

### 3. Set up Repository Secrets

In your source repository:
1. Go to Settings → Secrets and variables → Actions
2. Add a new repository secret:
   - Name: `SYNC_TOKEN`
   - Value: Your personal access token

### 4. Configure Target Repository

Choose one of these two configuration methods:

#### Option A: Using .env File (Recommended)

Create a `.env` file in the root of your source repository:



#### Option B: Using Repository Secrets

If you prefer not to commit a .env file, add this secret instead:
- Name: `TARGET_REPO_URL`
- Value: `https://github.com/username/target-repo.git`

<br>

## 🔄 Branch Logic

The workflow follows these rules for determining which branch to use in the target repository:

1. If `TARGET_BRANCH` is specified in the .env file:
   - Use that branch regardless of which branch you're pushing to
   
2. If no `TARGET_BRANCH` is specified AND source branch is 'main':
   - Use 'RepoBot' branch in the target repository
   
3. If no `TARGET_BRANCH` is specified AND source branch is not 'main':
   - Use the same branch name as the source

<br>

## 📊 Sync Status

After each sync, a `sync-status.md` file is created in the target repository with detailed information about:

- When the sync occurred
- Latest commit details
- Branch information
- Repository links

<br>

## ⚙️ Manual Triggering

You can manually trigger a sync from the Actions tab in your repository:

1. Go to the Actions tab
2. Select "Sync Repositories" workflow
3. Click "Run workflow"
4. Optionally enable force push
5. Click "Run workflow" button

<br>

## 🤝 Co-Author Support

You can add multiple co-authors to commits made by the sync bot. This is useful for:

- Properly attributing contributions when syncing collaborative work
- Ensuring commit history reflects all contributors
- Maintaining accurate authorship in mirrored repositories

To add co-authors, include them in the `.env` file:
```
CO_AUTHORS="Example1 <example1@example.com>, Example2 <example2@example.com>"
```

<br>

## 🔒 Security Considerations

- The sync token should have the minimal permissions needed
- Never commit your personal access token to the repository
- Consider using a dedicated bot account for syncing if you're syncing many repositories

<br>

## ✨ How to Use This Project

1. **Fork or Clone**: Fork this repository or clone it to your local machine to get started

2. **Customize the Workflow**: Modify the workflow file if needed to match your specific requirements

3. **Setup Authentication**: 
   - Create a Personal Access Token with appropriate permissions
   - Add the token as a repository secret named `SYNC_TOKEN`

4. **Configure Target Repository**:
   - Create a `.env` file with your target repository details
   - Example:
     ```
     TARGET_REPO_URL=https://github.com/Saviru/your-target-repo.git
     TARGET_BRANCH=target-branch
     CO_AUTHORS="Example1 <example1@example.com>, Example2 <example2@example.com>"
     ```

5. **Test the Workflow**:
   - Push a change to your repository
   - Go to the Actions tab to see the workflow run
   - Check the target repository to verify the sync

6. **Monitor and Maintain**:
   - Review the sync-status.md file in your target repository
   - Occasionally check that syncs are working as expected
   - Update your token if it expires

<br>

## 🛠️ Troubleshooting <hr>

**Issue**: Workflow fails with authentication errors
- **Solution**: Verify your SYNC_TOKEN has the correct permissions.

**Issue**: Files aren't syncing correctly
- **Solution**: Check the workflow run logs for errors and verify your .env configuration.

**Issue**: Workflow files not syncing
- **Solution**: Your token needs the `workflow` scope to sync workflow files.

**Issue**: Co-authors not appearing in commits
- **Solution**: Ensure the CO_AUTHORS format is correct with name and email in angle brackets.


<br>

## 🚀 Advanced Usage <hr>

### Custom Branch Mapping

For more complex branch mapping requirements, modify the workflow file's branch logic section to implement custom mapping rules.

<br>

## 📄 License <hr>

This project is licensed under the GNU General Public License v3.0 - see the LICENSE file for details.

###### Copyright © 2025 Saviru Kashmira Atapattu

<br>

## 🙏 Credits <hr>

Developed and maintained by [@Saviru](https://github.com/Saviru)
<br><br>
<hr>
<p align="center">Made with ❤️ for the GitHub community </p> 
