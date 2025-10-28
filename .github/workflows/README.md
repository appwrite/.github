# Reusable Workflows

This directory contains reusable workflows that can be used across repositories in the Appwrite organization.

## Stale Issues Workflow

The `stale.yml` workflow automatically marks inactive issues as stale and closes them after a specified period.

### Usage

To use this workflow in your repository, create a workflow file (e.g., `.github/workflows/stale.yml`) with the following content:

```yaml
name: Mark stale issues

on:
  schedule:
    - cron: "0 0 * * *"  # Run daily at midnight

jobs:
  stale:
    uses: appwrite/.github/.github/workflows/stale.yml@main
```

### Customization

You can customize the workflow behavior by providing inputs:

```yaml
name: Mark stale issues

on:
  schedule:
    - cron: "0 0 * * *"  # Run daily at midnight

jobs:
  stale:
    uses: appwrite/.github/.github/workflows/stale.yml@main
    with:
      stale-issue-message: 'This issue has been inactive for 30 days and will be closed soon.'
      days-before-stale: 30
      days-before-close: 7
      only-labels: 'question,needs-info'
```

### Available Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `stale-issue-message` | Message to post on issues when marking them as stale | No | "This issue has been labeled as a 'question', indicating that it requires additional information from the requestor. It has been inactive for 7 days. If no further activity occurs, this issue will be closed in 14 days." |
| `stale-issue-label` | Label to apply to stale issues | No | `stale` |
| `days-before-stale` | Number of days of inactivity before an issue is marked as stale | No | `7` |
| `days-before-close` | Number of days of inactivity before a stale issue is closed | No | `14` |
| `remove-stale-when-updated` | Remove stale label when an issue is updated | No | `true` |
| `close-issue-message` | Message to post on issues when closing them | No | "This issue has been closed due to inactivity. If you still require assistance, please provide the requested information." |
| `close-issue-reason` | Reason for closing the issue (`completed`, `not_planned`, `reopened`) | No | `not_planned` |
| `operations-per-run` | Maximum number of operations per run | No | `100` |
| `only-labels` | Only process issues with these labels (comma separated) | No | `question` |

## Auto-close External Pull Requests Workflow

The `autoclose.yml` workflow automatically closes pull requests from external contributors (non-organization members) with a message explaining that the repository is auto-generated.

### Usage

To use this workflow in your repository, create a workflow file (e.g., `.github/workflows/autoclose.yml`) with the following content:

```yaml
name: Auto-close External Pull Requests

on:
  pull_request:
    types: [opened]

jobs:
  auto_close:
    uses: appwrite/.github/.github/workflows/autoclose.yml@main
    secrets:
      GH_AUTO_CLOSE_PR_TOKEN: ${{ secrets.GH_AUTO_CLOSE_PR_TOKEN }}
```
