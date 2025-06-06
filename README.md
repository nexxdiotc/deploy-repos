# Slack Notifier – GitHub Actions Reusable Workflow

This repository contains a reusable GitHub Actions workflow for sending deployment notifications to Slack.

## 🔔 What it does

Sends a formatted message to a Slack channel via webhook when called from another workflow. It can notify on deployment `start`, `success`, or `failure`.

## 🧩 How to use it

In your workflow (from another repo):

```yaml
jobs:
  notify:
    uses: nexxdiotc/deploys-repos/.github/workflows/slack-notifier.yml@main
    with:
      status: start             # Options: start, success, failure
      environment: production   # e.g., staging, qa, production
      repository: ${{ github.repository }}
      commit_sha: ${{ github.sha }}
      commit_url: https://github.com/${{ github.repository }}/commit/${{ github.sha }}
      image_uri: my-registry/image:tag
    secrets:
      SLACK_WEBHOOK_URL: ${{ secrets.SLACK_WEBHOOK_URL }}

