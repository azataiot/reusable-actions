# Reusable github actions

[![Code Quality](https://github.com/azataiot/python-project-template/actions/workflows/code-quality.yml/badge.svg)](https://github.com/azataiot/python-project-template/actions/workflows/code-quality.yml)
[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit)](https://github.com/pre-commit/pre-commit)
[![security: bandit](https://img.shields.io/badge/security-bandit-yellow.svg)](https://github.com/PyCQA/bandit)
[![latest release](https://img.shields.io/github/v/release/azataiot/reusable-actions)](https://github.com/azataiot/reusable-actions/releases)

**Introduction**: Some personal collection of reusable actions to reuse and call in other actions.

## Usage

```yml
name: Code Quality

on:
  pull_request:
    branches: [ 'main', 'dev' ]
    types:
      - opened
      - synchronize
  push:
    branches: [ 'dev' ]
  workflow_dispatch:
    if: github.actor != 'dependabot[bot]'

permissions:
  contents: read

jobs:
  linting:
    uses: azataiot/reusable-actions/.github/workflows/reusable-python.yaml@dev
    with:
      run-pre-commit: true
      run-py-test: true
      run-pypi-publish: false

```

```yml
name: Github Release

on:
  pull_request:
    branches: [ 'main' ]
    types:
      - closed
  workflow_dispatch:

jobs:
  github-release:
    permissions:
      issues: write
      pull-requests: write
      contents: write
    if: github.event.pull_request.merged == true && github.repository_owner == 'azataiot'
    uses: azataiot/reusable-actions/.github/workflows/reusable-release.yaml@dev
    with:
      debug: true
      create-issue: true
      fail-if-release-exists: true

```





## Contributing

Contributions are always welcome! Whether it's bug reports, feature requests, or pull requests, all contributions are
appreciated. For more details, see [CONTRIBUTING.md](CONTRIBUTING.md).

## License

This project is licensed under some License. For more details, see [LICENSE](LICENSE.md).

## Code of Conduct

We believe in fostering an inclusive and respectful community. For guidelines and reporting information,
see [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md).

## Security

Your security is paramount. If you discover any security-related issues, please follow the guidelines
in [SECURITY.md](SECURITY.md).

## Founding

For information about the project's founding and backers, see [FOUNDING](https://github.com/sponsors/azataiot).
