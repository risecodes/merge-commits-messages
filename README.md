# Merge-commits-messages 📟

A GitHub Action that get commits messages that relates to Jira stories 
and update the PR description with the relevant Jira stories

## Motivation

Jira and github has a deployment integration so that when using GitHub action
to deploy code, the relevant Jira story get's updated according to the relevant environment.
To do this, the commits message/ branch name/ Pr description must contain the Jira story Id.
However, when creating a PR from `staging` branch to `production` branch for example. the Jira ticket loss
context, and you'll have to manually update the PR description with the relevant Story ID.

This is where *Merge-commits-messages* action comes in.


## Usage
Add .github/workflows/merge-commits-messages.yml with the following:

```
name: merge-commits-messages
on:
  pull_request:
    types: [opened]
    branches:
      - 'production'

jobs:
  commits_to_pr_job:
    runs-on: ubuntu-latest
    name: get-pr-commits
    steps:
      - name: Checkout
      - uses: actions/checkout@v3
      - name: Get PR Commits & Update description
      - uses: risecodes/merge-commits-messages@main
        with:
          repository: risecodes/merge-commits-messages
          token: ${{ secrets.GITHUB_TOKEN }}
        run: npm start
```
