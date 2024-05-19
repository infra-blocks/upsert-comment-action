# composite-action-template
[![Release](https://github.com/infra-blocks/composite-action-template/actions/workflows/release.yml/badge.svg)](https://github.com/infra-blocks/composite-action-template/actions/workflows/release.yml)
[![Self Test](https://github.com/infra-blocks/composite-action-template/actions/workflows/self-test.yml/badge.svg)](https://github.com/infra-blocks/composite-action-template/actions/workflows/self-test.yml)
[![Trigger Update From Template](https://github.com/infra-blocks/composite-action-template/actions/workflows/trigger-update-from-template.yml/badge.svg)](https://github.com/infra-blocks/composite-action-template/actions/workflows/trigger-update-from-template.yml)

[//]: # ([![Update From Template]&#40;https://github.com/infra-blocks/composite-action-template/actions/workflows/update-from-template.yml/badge.svg&#41;]&#40;https://github.com/infra-blocks/composite-action-template/actions/workflows/update-from-template.yml&#41;)

Template repository for GitHub Actions using the composite engine. Upon instantiating, go through the following checklist:

- Do a global search & replace for `composite-action-template` and replace it with the name of your repository
- Remove the [trigger-update-from-template workflow](.github/workflows/trigger-update-from-template.yml)
- Replace the `Trigger Update From Template` status badge for the `Update From Template` status badge.
- Edit the action.yml to correspond to your new action
- Edit the self-test workflow.
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
      - uses: infra-blocks/composite-action-template@v1
```
