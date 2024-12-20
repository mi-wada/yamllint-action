# yamllint-action

GitHub Actions to execute [yamllint](https://github.com/adrienverge/yamllint).

## Usage

```yaml
name: yamllint
on:
  push:
    branches:
      - main
  pull_request:
jobs:
  yamllint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: mi-wada/yamllint-action@v1
        with:
          yamllint_flags: .
```
