![Actions Status](https://github.com/machine-learning-apps/kubeflow-triage/workflows/Tests/badge.svg)

# Triage Issues For Kubeflow
A GitHub Action that triages issues for the [Kubeflow](https://github.com/kubeflow/) project.

## Discussion

- [Notebook](https://github.com/kubeflow/code-intelligence/blob/master/Issue_Triage/notebooks/triage.ipynb) exploring ways to programatically triage issues.
- [Issue](https://github.com/kubeflow/community/issues/278) describing requirements for automatic triage.

# Usage

## Example Workflow

```yaml
name: Issue-Triage
on: 
  issues:
    types: [opened, closed, reopened, transferred, labeled, unlabeled]
    # Issue is created, Issue is closed, Issue added or removed from projects, Labels added/removed

jobs:
  triage:
    runs-on: ubuntu-latest
    steps:
      - name: Triage Issue
        uses: machine-learning-apps/kubeflow-triage@master
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          PROJECT_CARD_ID: 1 #test id
          ISSUE_NUMBER: ${{ github.event.issue.number }}
```

## Mandatory Inputs

1. `PROJECT_CARD_ID`: The Project Card ID that you want to move issues to.
2. `ISSUE_NUMBER`: The issue number in the current repo that you want to triage

**Also, you must supply the GITHUB_TOKEN from the Action environment as an environment variable**, which can be accomplished like so:

```yaml
env:
  GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
``
