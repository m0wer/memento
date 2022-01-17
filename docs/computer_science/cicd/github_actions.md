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

# Configuration

## Concurrency

You can use `concurrency` to cancel any in-progress job or run. Example:

```yaml
concurrency:
  group: docs-${{ github.head_ref }}
  cancel-in-progress: true
```

This is useful to cancel previous jobs if new commits are pushed, which saves
minutes, energy and avoids conflicts when pushing changes during the action.

## Secrets

### Store file as secret

If you want to store a file (multiline, binary...) as a secret, first encode it
with base64:

```bash
base64 -i < {{ file_path }} | tr -d '\n' | xclip -i -selection clipboard
```

Then paste it to a new secret. To restore the file diring the workflow, add:

```yaml
- name: restore file
  run: echo ${{ secrets.SECRET }} | base64 -d > {{ file_path }}
```

## Steps

### Condition execution depending on another step outcome

To allow a step to fail without that implying failing the whole
workflow and then execute some steps according to the result, do:

```yaml
- name: commitizen
  id: commitizen
  continue-on-error: true
  uses: commitizen-tools/commitizen-action@0.11.0
  with:
    github_token: ${{ secrets.GITHUB_TOKEN }}

- name: Some other task
  if: steps.commitizen.outcome == 'success'
  run: something
```
