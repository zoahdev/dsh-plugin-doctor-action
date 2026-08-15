# dsh-plugin-doctor-action

> A GitHub Action that runs pre-publish health checks on any DeepSeek Harness plugin - powered by [dsh-plugin-doctor](https://github.com/zoahdev/dsh-plugin-doctor).

One line in your workflow turns "it loads" into "it is checked": manifest structure, patch validity, entry points, files allowlist, and (optionally) a full build + pack + fresh-profile install smoke.

## Usage

```yaml
name: plugin
on: [push, pull_request]

jobs:
  doctor:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: zoahdev/dsh-plugin-doctor-action@v1
        with:
          path: .
          # full: 'true'   # add build + pack + fresh-profile install smoke
```

## Inputs

| Input | Default | Meaning |
| --- | --- | --- |
| `path` | `.` | Plugin directory to check |
| `version` | `v1.13.0` | dsh-plugin-doctor release tag to install |
| `full` | `false` | Also run `--full` (build + pack + fresh-profile install) |

## Outputs

| Output | Meaning |
| --- | --- |
| `ok` | `true` when the plugin passed |

Failures and warnings are also surfaced as GitHub annotations (`::error::` / `::warning::`) and written to the run summary.

## Why

The DeepSeek Harness ecosystem ships plugins as source checkouts, npm packages, and GitHub tarballs - and "loads" is not "callable" (discussions #1965, #1697, #2002). This action makes the same checks the maintainers would run available to every plugin author before a user ever installs it.

## License

MIT
