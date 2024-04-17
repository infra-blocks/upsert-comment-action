# composite-action-template
[![Release](https://github.com/infrastructure-blocks/composite-action-template/actions/workflows/git-tag-semver-from-label.yml/badge.svg)](https://github.com/infrastructure-blocks/composite-action-template/actions/workflows/git-tag-semver-from-label.yml)
[![Self Test](https://github.com/infrastructure-blocks/composite-action-template/actions/workflows/self-test.yml/badge.svg)](https://github.com/infrastructure-blocks/composite-action-template/actions/workflows/self-test.yml)
[![Update Template Instances](https://github.com/infrastructure-blocks/composite-action-template/actions/workflows/trigger-update-from-template.yml/badge.svg)](https://github.com/infrastructure-blocks/composite-action-template/actions/workflows/trigger-update-from-template.yml)

Upon creating a repository from this template:
- Remove the [trigger-update-from-template workflow](.github/workflows/trigger-update-from-template.yml)
- Add the [update-from-template](.github/workflows/update-from-template.yml) status badge.
- Edit the action.yml to correspond to your new action
- Edit the self-test workflow.
- Update the status badges:
  - Remove the `Trigger Update From Template` status badge.
  - Add the `Update From Template` status badge.
  - Rename the rest of the links to point to the right repository.
- Edit this readme: this summary and the usage section.

## Inputs

|     Name      | Required | Description       |
|:-------------:|:--------:|-------------------|
| example-input |   true   | An example input. |

## Outputs

|      Name      | Description        |
|:--------------:|--------------------|
| example-output | An example output. |

## Permissions

|     Scope     | Level | Reason   |
|:-------------:|:-----:|----------|
| pull-requests | read  | Because. |

## Usage

```yaml
name: Template Usage

on:
  push: ~

# The required permissions.
permissions:
  pull-requests: read

# The suggested concurrency controls.
concurrency:
  group: ${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true

jobs:
  example-job:
    runs-on: ubuntu-22.04
    steps:
      - uses: infrastructure-blocks/composite-action-template@v1
```
