# yamllint-action

GitHub Actions for running [yamllint](https://github.com/adrienverge/yamllint) with [reviewdog](https://github.com/reviewdog/reviewdog?tab=readme-ov-file#installation). This action supports linting only the YAML files that have changed in a pull request.

This GitHub Action is simply an enhanced version of <https://github.com/reviewdog/action-yamllint> with the addition of the `only_changed` option.

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

## Inputs

### `yamllint_flags`

Optional. Default is blank. Flags and args of yamllint command. It works like this:

```shell
yamllint ${{ inputs.yamllint_flags }}
```

When using with `only_changed`, it works like this:

```shell
yamllint ${{ inputs.yamllint_flags }} CHANGED_FILE1 CHANGED_FILE2
```

### `only_changed`

Optional. Default is `false`. If `true`, lint only changed(added/modified) files in a pull request.

It works only on `pull_request` or `pull_request_target` event. If working on other events, it will lint all files.

### `github_token`

Optional. Default is `${{ github.token }}`.

### `level`

Optional. Default is `error`. Report level for reviewdog [info,warning,error].
It's same as `-level` flag of reviewdog.

### `reporter`

Optional. Default is `github-pr-check`. Reporter of reviewdog command [github-pr-check,github-check,github-pr-review].
It's same as `-reporter` flag of reviewdog.

`github-pr-review` can use Markdown and add a link to rule page in reviewdog reports.

### `filter_mode`

Optional. Default is `added`. Filtering mode for the reviewdog command [added,diff_context,file,nofilter].

### `fail_level`

Optional. Default is `none`. If set to `none`, always use exit code 0 for reviewdog.
Otherwise, exit code 1 for reviewdog if it finds at least 1 issue with severity greater than or equal to the given level.
Possible values: [`none`, `any`, `info`, `warning`, `error`]

### `reviewdog_flags`

Optional. Default is blank. Additional reviewdog flags.
