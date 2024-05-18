# upsert-comment-action
[![Release](https://github.com/infra-blocks/upsert-comment-action/actions/workflows/git-tag-semver-from-label.yml/badge.svg)](https://github.com/infra-blocks/upsert-comment-action/actions/workflows/git-tag-semver-from-label.yml)
[![Self Test](https://github.com/infra-blocks/upsert-comment-action/actions/workflows/self-test.yml/badge.svg)](https://github.com/infra-blocks/upsert-comment-action/actions/workflows/self-test.yml)
[![Update From Template](https://github.com/infra-blocks/upsert-comment-action/actions/workflows/update-from-template.yml/badge.svg)](https://github.com/infra-blocks/upsert-comment-action/actions/workflows/update-from-template.yml)

This action creates/updates a comment that matches a specific pattern. The comment author is expected to be
the GitHub Actions bot. When posting a comment that matches an existing comment, it overwrites it.

## Inputs

|     Name     | Required | Description                                                                                                                   |
|:------------:|:--------:|-------------------------------------------------------------------------------------------------------------------------------|
|     body     |   true   | The comment content                                                                                                           |
|   matches    |   true   | The regular expression used to find existing comment. If one is found, it is updated. A new comment is created otherwise.     |
| issue-number |   true   | The issue where to post the comment. This defaults to the PR number on pull request events, otherwise, it should be provided. | 

## Outputs

|    Name    | Description     |
|:----------:|-----------------|
| comment-id | The comment ID. |

## Permissions

|     Scope     | Level | Reason                                      |
|:-------------:|:-----:|---------------------------------------------|
| pull-requests | write | Required to post comments on pull requests. |

## Usage

### Inferring issue from current PR
```yaml
name: Upsert Comment Action

on:
  pull_request: ~

permissions:
  pull-requests: write

jobs:
  upsert-comment:
    runs-on: ubuntu-22.04
    steps:
      # Defaults to using ${{ github.event.pull_request.number }}
      - id: upsert-comment
        uses: infra-blocks/upsert-comment-action@v1
        with:
          body: |
            What's up bro?
          matches: "^What's up"
      - run: |
          echo "Comment created: ${{ steps.upsert-comment.outputs.comment-id }}"
```

### Explicitly passing issue-number
```yaml
name: Upsert Comment Action

on:
  push: ~

permissions:
  pull-requests: write

jobs:
  upsert-comment:
    runs-on: ubuntu-22.04
    steps:
      # Gets the PR from the GITHUB_SHA on push.
      - id: get-current-pr
        uses: infra-blocks/get-current-pull-request-action@v1
      # Upsert a comment on the issue (PR in our case) number
      - id: upsert-comment
        uses: infra-blocks/upsert-comment-action@v1
        with:
          issue-number: ${{ steps.get-current-pr.outputs.number }}
          body: |
            What's up sis?
          matches: "^What's up"
      - run: |
          echo "Comment created: ${{ steps.upsert-comment.outputs.comment-id }}"
```
