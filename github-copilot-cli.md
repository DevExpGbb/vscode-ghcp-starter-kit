# GitHub Copilot CLI Useage


```bash
npm install -g @github/copilot

# Use GitHub CLI Auth
# Login as prompted

gh auth login

## ---- OR ---- 

# use a GitHub Personal Access Token (PAT) - "good" for automation/scripting

export GITHUB_TOKEN="your_github_token_here"


## Run a command
copilot -p "Generate a Python function that takes a list of integers and returns the sum of the even numbers in the list."
```