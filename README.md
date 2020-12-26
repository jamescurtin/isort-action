# isort Github Action

This action runs isort on a Python repository.

It requires that the [`checkout`][github-checkout] and [`setup-python`][github-setup-python] actions be used first.

## Inputs

### `isortVersion`

Optional. Version of `isort` to use. Defaults to latest version of `isort`.

### `sortPaths`

Optional. List of paths to sort, relative to your project root. Defaults to `.`

### `configuration`

Optional. `isort` configuration options to pass to the `isort` CLI. Defaults to `-check-only --diff`.

### `requirementsFiles`

Optional. Paths to python requirements files to install before running isort.
If multiple requirements files are provided, they should be separated by a space.
If custom package installation is required, dependencies should be installed in a separate step before using this action.

## Outputs

### `isort-result`

Output of the `isort` CLI.

## Example usage

```yaml
name: Run isort
on:
  - push

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-python@v2
        with:
          python-version: 3.9
      - uses: isort/isort-action@master
        with:
            requirementsFiles: "requirements.txt requirements-test.txt"
```

## Developing

Before starting on a new feature, please review the [contributing guide][contributors-guide].

All PRs must pass the CI pipeline to be merged.
To validate your code, you may run the test suite locally using `docker-compose`.
The full test suite can be run via `docker-compose run --rm lint`, which will auto-format the code
or add the `--check-only` flag to exit without formatting code.

[contributors-guide]: CONTRIBUTING.md
[github-checkout]: https://github.com/actions/checkout
[github-setup-python]: https://github.com/actions/setup-python
