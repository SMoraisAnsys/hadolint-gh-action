# Hadolint-action

A github action that checks your Dockerfile with [hadolint][hadolint]. It supports a variety of options as well as annotating your Dockerfile with said results.

## Usage

```yaml
name: "Hadolint"
description: "Analyze Dockerfile with Hadolint"
runs:
  steps:
    - uses: actions/checkout@v2
    - run: jbergstroem/hadolint-gh-action@v1
```

## Parameters

| Variable      | Default        | Description                                                                                                                  |
| :------------ | :------------- | :--------------------------------------------------------------------------------------------------------------------------- |
| dockerfile    | `./Dockerfile` | Path to Dockerfile. Accepts shell expansions (`**/Dockerfile`)                                                               |
| config_file   |                | Path to optional config (hadolint defaults to read `./hadolint.yml` if it exists)                                            |
| error_level   | `0`            | Fail CI if hadolint emits output (`-1`: never, `0`: error, `1`: warning, `2`: info)                                          |
| annotate      | true           | Annotate code inline in the github PR viewer (`true`/`false`)                                                                |
| output_format | `json`         | Use with output_file to set output format (choose between `tty`, `json`, `checkstyle`, `codeclimate` or `gitlab_codeclimate` |

## Hadolint version

The variable `hadolint_version` will always contain what version the action is running.
This can be useful in debugging scenarios where things "break" from one day to the other due to the action being updated.

## Output

You can control the behavior of how hadolint presents its findings by configuring:

- annotate: let feedback show inline in your code review
- output_format: store the output in a variable you can pass on to other processing tools

If `output_format` is set, the github action variable `hadolint_output` will be set. You can choose what format you prefer depending on how you want to process the results.

## Robustness

Also known as "can I run this in production". The action itself is tested via CI for all its use cases as well as unit tests for each function. Additionally, `shellcheck` is run against all shell scripts. Releases are cut manually (for now) and the action will strictly follow semver with regards to breaking functionality or options.