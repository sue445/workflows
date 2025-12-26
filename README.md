# workflows
[Reusable workflows](https://docs.github.com/en/actions/how-tos/reuse-automations/reuse-workflows) for GitHub Actions

[![test](https://github.com/sue445/workflows/actions/workflows/test.yml/badge.svg)](https://github.com/sue445/workflows/actions/workflows/test.yml)

## [dependabot-auto-merge.yml](.github/workflows/dependabot-auto-merge.yml)
Auto-merge Dependabot PR

> [!IMPORTANT]
> Requires followings
> 
> * [Allow auto-merge](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/managing-auto-merge-for-pull-requests-in-your-repository#managing-auto-merge)
> * Enable [Require status checks before merging](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches#require-status-checks-before-merging) and add checks to "Status checks that are required"

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
      # slack-webhook: ${{ secrets.SLACK_WEBHOOK }}
```

## [pages-yard.yml](.github/workflows/pages-yard.yml)
Deploy yard to Pages

e.g.

```yml
name: pages-yard

on:
  push:
    branches:
      - main
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  deploy:
    uses: sue445/workflows/.github/workflows/pages-yard.yml@main
    # with:
    #   ruby-version: ruby
    #   bundle-without: production
    #   before-command: |
    #     sudo apt-get update
    #     sudo apt-get install -y libgda-5.0
    # secrets:
    #   slack-webhook: ${{ secrets.SLACK_WEBHOOK }}
```

## [rbs-collection-updater.yml](.github/workflows/rbs-collection-updater.yml)
Run `rbs collection update` and create Pull Request for `rbs_collection.lock.yaml`

> [!IMPORTANT]
> Requires followings when enabling `auto-merge`
>
> * [Allow auto-merge](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/managing-auto-merge-for-pull-requests-in-your-repository#managing-auto-merge)
> * Enable [Require status checks before merging](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches#require-status-checks-before-merging) and add checks to "Status checks that are required"

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
    # with:
    #   assignees: sue445
    #   auto-merge: true
    #   ruby-version: ruby
    secrets:
      app-id: ${{ secrets.GH_APP_ID }}
      private-key: ${{ secrets.GH_APP_PRIVATE_KEY }}
      # slack-webhook: ${{ secrets.SLACK_WEBHOOK }}
```
