# upsert-comment-action

This action creates/updates a comment that matches a specific pattern. The comment author is expected to be
the GitHub Actions bot. When posting a comment that matches an existing comment, it overwrites it.

## Usage

### Inferring issue from current PR
```yaml
name: Upsert Comment Action

on:
  pull_request: ~

jobs:
  upsert-comment:
    runs-on: ubuntu-22.04
    steps:
      - id: upsert-comment
        uses: infrastructure-blocks/upsert-comment-action@v1
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

jobs:
  upsert-comment:
    runs-on: ubuntu-22.04
    steps:
      # Gets the PR from the GITHUB_SHA
      - id: get-current-pr
        uses: 8BitJonny/gh-get-current-pr@2.2.0
      - id: upsert-comment
        uses: infrastructure-blocks/upsert-comment-action@v1
        with:
          issue-number: ${{ steps.get-current-pr.outputs.number }}
          body: |
            What's up sis?
          matches: "^What's up"
      - run: |
          echo "Comment created: ${{ steps.upsert-comment.outputs.comment-id }}"
```

## Development

### Releasing

The releasing is handled at git level with semantic versioning tags. Those are automatically generated and managed
by the [git-tag-semver-from-label-workflow](https://github.com/infrastructure-blocks/git-tag-semver-from-label-workflow).
