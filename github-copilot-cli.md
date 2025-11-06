# GitHub Copilot CLI Useage

## Installation

## Authentication

```bash
npm install -g @github/copilot

```

### Use GitHub CLI Auth

Good for local single user/synchronous work in CLI

```bash
gh auth login
```

### Using a GitHub Personal Access Token (PAT)

This method is "good" for automation/scripting/async work at scale.  

> [!NOTE]
> Would be better if we can leverage a GitHu Action Runner ```GITHUB_TOKEN``` but that's not possible today.

```bash
export GITHUB_TOKEN="your_github_token_here"
```

## Run a command
```bash

copilot -p "Generate a Python function that takes a list of integers and returns the sum of the even numbers in the list."
```