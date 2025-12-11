# workflows
[Reusable workflows](https://docs.github.com/en/actions/how-tos/reuse-automations/reuse-workflows) for GitHub Actions

## [dependabot-auto-merge.yml](.github/workflows/dependabot-auto-merge.yml)
e.g.

```yml
name: dependabot-auto-merge

on:
  pull_request:
    types:
      - opened
      - synchronize # PR branch is rebased

jobs:
  auto-merge:
    uses: sue445/workflows/.github/workflows/dependabot-auto-merge.yml@main
    secrets:
      # TODO: Set secrets to Dependabot secrets
      app-id: ${{ secrets.GH_APP_ID }}
      private-key: ${{ secrets.GH_APP_PRIVATE_KEY }}
      slack-webhook: ${{ secrets.SLACK_WEBHOOK }}
```

## [rbs-collection-updater.yml](.github/workflows/rbs-collection-updater.yml)
e.g.

```yml
name: rbs-collection-updater

on:
  schedule:
    - cron: "0 0 1 * *" # Run monthly
  workflow_dispatch:

jobs:
  build:
    uses: sue445/workflows/.github/workflows/rbs-collection-updater.yml@main
    with:
      assignees: sue445
    secrets:
      app-id: ${{ secrets.GH_APP_ID }}
      private-key: ${{ secrets.GH_APP_PRIVATE_KEY }}
      slack-webhook: ${{ secrets.SLACK_WEBHOOK }}
```
