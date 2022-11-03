[![star this repo][gh-stars-image]][gh-url] [![fork this repo][gh-forks-image]][gh-url] [![Build Status][gh-status-image]][gh-url]

# gh-workflows

> A collection of reusable workflows for GitHub Actions.

Here some reusable workflows are shared. The main purpose of this repository is for usage on repositories hosted on @jenssimon. But if you find something useful please feel free to use it outside of this context.

## skip-push-pr-duplicates

This workflow checks if a run of CI tasks is necessary in workflows that uses both `push` and `pull_request`. So it helps to skip duplicate runs.

**Usage:**

```yaml
name: Test

on:
  push:
    branches: [ '**' ]
  pull_request:
    branches: [ main ]

jobs:
  pre_job:
    uses: jenssimon/gh-workflows/.github/workflows/skip-push-pr-duplicates.yml@v1.0.1

  build:
    needs: pre_job
    if: ${{ needs.pre_job.outputs.needs_run_and_release == 'true' }}
    # ...
```

**Outputs:**

| Name                    | Type      | Description                                                                                              |
|:------------------------|:----------|:---------------------------------------------------------------------------------------------------------|
| `needs_run`             | `boolean` | Returns `true` if a run of CI jobs is necessary.                                                         |
| `needs_run_and_release` | `boolean` | Same as `needs_run` but it also returns `true` when the current workflow is a `push` to the main branch. |

## License

MIT © 2022 [Jens Simon](https://github.com/jenssimon)

[gh-url]: https://github.com/jenssimon/gh-workflows
[gh-stars-image]: https://badgen.net/github/stars/jenssimon/gh-workflows
[gh-forks-image]: https://badgen.net/github/forks/jenssimon/gh-workflows
[gh-status-image]: https://badgen.net/github/status/jenssimon/gh-workflows
