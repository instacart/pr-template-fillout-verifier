# PR Template Fillout Verifier

A simple Github action which allows several different actions be taken when a PR body is determined to be identical to the PR template.

## Permissions

`contents: read` is required to read the PR template

`contents: write` is required for converting a PR to a Draft

`pull-requests: write` is required to comment on the PR

## Parameters

See [https://github.com/foursquare/pr-template-fillout-verifier/blob/main/action.yaml#L3](https://github.com/foursquare/pr-template-fillout-verifier/blob/main/action.yaml#L3).


## Example Usage

```yaml
name: Check that PR was filled out

on:
  pull_request_target:
    types: [ opened, reopened, ready_for_review, edited ]

jobs:
  check_pr_description:
    runs-on: ubuntu-20.04
    permissions:
      contents: write
      pull-requests: write
    steps:
      - id: check-pr
        uses: foursquare/pr-template-fillout-verifier@v0.0.3
        if: github.event.pull_request.draft == false
        with:
          comment: 'Please fill out the PR template'
          fail: "true"
          convert-to-draft: "true"
          template-path: ".github/pull_request_template.md"
```
 
