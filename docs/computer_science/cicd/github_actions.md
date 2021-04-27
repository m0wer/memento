---
title: GitHub Actions
date: 2021-04-27
author: m0wer
tags: [ 'cicd', 'github' ]
---

[GitHub Actions](https://github.com/features/actions) let's you automate,
customize, and execute your software development workflows right in your
repository.

# Actions

## Checkout V2

[actions/checkout](https://github.com/actions/checkout)is an action for
checking out a repo.

Example usage:

```yaml
jobs:
  molecule:
    runs-on: ubuntu-latest
    strategy:
      fail-fast: false
    steps:
      - name: Checkout
        uses: actions/checkout@v2
        with:
          submodules: true
```

## GitHub Action for GitHub Push

[ad-m/github-push-action](https://github.com/ad-m/github-push-action)is a
GitHub action to push back to repository eg. update code.

Example usage:

```yaml
jobs:
  molecule:
    runs-on: ubuntu-latest
    strategy:
      fail-fast: false
    steps:
      - name: Push changes
        uses: ad-m/github-push-action@master
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          branch: ${{ github.ref }}
```

This will push the commited changes to the current branch.
