# cfn-nag-sarif GitHub Action

This action executes cfn_nag_scan linter against the repo for which the workflow is run and uploads the result to GitHub's Code Scanning

For more background on the tool, chechout [cfn_nag repo](https://github.com/stelligent/cfn_nag).

## Usage
Scan all the cloudformation templates in `templates` on the default branch. Replace `$default-branch` with the name of the default branch in your repo.

```
name: cfn-nag

on:
  push:
    branches: [ $default-branch ]
  pull_request:
    branches: [ $default-branch ]
  schedule:
    -cron: $cron-weekly

jobs:
  cfn-nag:
    name: Run cfn-nag scan
    runs-on: ubuntu-latest
    permissions:
      actions: read
      contents: read
      security-events: write

    steps:
      - name: Clone repo
        uses: actions/checkout@v2

      - name: Run cfn-nag
        uses: stelligent/cfn-nag-sarif-action@v1
        with:
          input_path: templates
```

## Inputs

### `input_path`

The directory of the repo to search for violations. Default: `$GITHUB_WORKSPACE`

### `extra_args`

Additional arguments to pass to `cfn_nag_scan`. See the [usage for `cfn_nag_scan`](https://github.com/stelligent/cfn_nag#usage) for details. Default: ``

## Support

To report a bug or request a feature, submit an issue through the GitHub repository via: https://github.com/stelligent/cfn-nag-sarif-action/issues/new

Pull requests are welcome as well: https://github.com/stelligent/cfn-nag-sarif-action/pulls