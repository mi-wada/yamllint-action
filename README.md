# yamllint-action

GitHub Actions for running [yamllint](https://github.com/adrienverge/yamllint) with [reviewdog](https://github.com/reviewdog/reviewdog?tab=readme-ov-file#installation). This action supports linting only the YAML files that have changed in a pull request.

## Usage

### Lint only changed YAML files

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
          only_changed: true
```

### Lint all YAML files

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

### Lint all YAML files under the specified directory

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
          yamllint_flags: ./path/to/directory
```
