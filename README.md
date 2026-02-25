# Datadog Code Coverage Upload Action

A GitHub Action to upload code coverage report files to [Datadog](https://docs.datadoghq.com/code_coverage/).

This action uses the [datadog-ci](https://github.com/DataDog/datadog-ci) standalone binary (installed via
[install-datadog-ci-github-action](https://github.com/DataDog/install-datadog-ci-github-action)), so **no Node.js
setup is required**.

## Usage

```yaml
name: Test Code
on: [push]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: make tests
      - uses: DataDog/coverage-upload-github-action@v2
        with:
          api_key: ${{ secrets.DD_API_KEY }}
```

### Upload with flags

```yaml
- uses: DataDog/coverage-upload-github-action@v2
  with:
    api_key: ${{ secrets.DD_API_KEY }}
    flags: "type:unit-tests,jvm-21"
```

### Specify report files path

```yaml
- uses: DataDog/coverage-upload-github-action@v2
  with:
    api_key: ${{ secrets.DD_API_KEY }}
    files: ./coverage
    ignored-paths: "**/vendor"
```

### Pin a specific datadog-ci version

```yaml
- uses: DataDog/coverage-upload-github-action@v2
  with:
    api_key: ${{ secrets.DD_API_KEY }}
    version: "v5.6.0"
```

## Inputs

| Name            | Description                                                                                                            | Required | Default         |
|-----------------|------------------------------------------------------------------------------------------------------------------------|----------|-----------------|
| `api_key`       | Datadog API key to use to upload the reports.                                                                          | Yes      |                 |
| `site`          | The [Datadog site](https://docs.datadoghq.com/getting_started/site/) to upload the reports to.                         | No       | `datadoghq.com` |
| `files`         | Directories, files, or glob patterns used when looking for coverage report files.                                      | No       | `.`             |
| `ignored-paths` | A comma-separated list of paths to exclude from report file discovery. Glob patterns are supported.                    | No       |                 |
| `flags`         | Flags for grouping and filtering (e.g., `type:unit-tests,jvm-21`). Comma-separated, max 32 per report.                | No       |                 |
| `format`        | Override the format of the coverage report files (auto-detected by default).                                           | No       |                 |
| `base-path`     | Base path (relative to repo root) for the file paths inside the coverage reports.                                      | No       |                 |
| `version`       | Version of `datadog-ci` to install. Use a major version like `v5` or a specific tag like `v5.6.0` to pin.             | No       | `v5`            |
| `extra-args`    | Extra args to be passed to the `datadog-ci coverage upload` command.                                                   | No       |                 |

## Supported platforms

This action supports all platforms supported by the `datadog-ci` standalone binary:

| Runner OS | Architecture |
|-----------|-------------|
| Linux     | X64, ARM64  |
| macOS     | X64, ARM64  |
| Windows   | X64         |

## License

Apache 2.0 - See [LICENSE](LICENSE) for details.
