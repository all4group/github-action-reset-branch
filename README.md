# GitHub Action: Reset branch

## Description

Action to reset branch to another branch.

## Requirements

Action does not require anything special to be installed on `runner`.

## Inputs

```
branch           - branch to reset (required, not set by default)

source           - source branch (required, not set by default)

protected        - protected branches (not required, defaults to "main,develop,release")
                   if you don't want to protect any branch set it to a value
                   that is not related to any branch name i.e. "protected: none"
```

## Outputs

```
none
```

## Usage

### Sample workflow definition

```
name: Sample workflow

on:
  workflow_dispatch:
    inputs:
      branch:
        description: "Branch to reset"
        required: true
      source:
        description: "Source branch"
        required: true
        default: "develop"

jobs:
  sample:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
        with:
          fetch-depth: 0
      - name: Initialize git
        run: |
          git config user.name github-actions
          git config user.email github-actions@github.com
        shell: bash
      - name: Execute action reset branch
        uses: all4group/github-action-reset-branch@v2
        with:
          branch: ${{ github.event.inputs.branch }}
          source: ${{ github.event.inputs.source }}
```
