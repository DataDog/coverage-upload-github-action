# Datadog Code Coverage Upload Action

This action downloads the [datadog-ci](https://github.com/DataDog/datadog-ci) and uses it to upload code coverage
reports to Datadog.

This action sets up node and requires node `>=14`. You can configure a specific version of node to use.
Note that if you have set up another version already it will override it.

## Usage

```yaml
name: Test Code
on: [ push ]
jobs:
  test:
    steps:
      - uses: actions/checkout@v3
      - run: make tests
      - uses: datadog/coverage-upload-github-action@v1
        with:
          api_key: ${{ secrets.DD_API_KEY }}
```

## Inputs

The action has the following options:

| Name                 | Description                                                                                                                 | Required | Default         |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------|----------|-----------------|
| `api_key`            | Datadog API key to use to upload the reports.                                                                               | True     |                 |
| `site`               | The Datadog site to upload the reports to.                                                                                  | False    | `datadoghq.com` |
| `files`              | Path to file or folder containing reports to upload                                                                         | False    | `.`             |
| `auto-discovery`     | Do a recursive search and automatic reports discovery in the folders provided in `files` input (current folder if omitted). | False    | `true`          |
| `ignored-paths`      | A comma-separated list of paths that are ignored when report files auto-discovery is done. Glob patterns are supported.     | False    |                 |
| `node-version`       | The node version to use to install the datadog-ci. It must be `>=14`                                                        | False    | `20`            |
| `datadog-ci-version` | Optionally pin the @datadog/datadog-ci version.                                                                             | False    | `latest`        |
| `extra-args`         | Extra args to be passed to the datadog-ci coverage upload command.                                                          | False    |                 |
