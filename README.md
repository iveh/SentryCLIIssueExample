# Background and Setup

## Issue encountered

Running `sentry-cli` with the `upload-proguard` subcommand from inside the `node_modules` results in no output at all.

Example command and output:

```
node_modules/@sentry/cli/bin/sentry-cli
```

By comparison, if the `upload-dif` subcommand is invoked, with no further arguments, it provides a useful error message:

```
node_modules/@sentry/cli/bin/sentry-cli upload-dif
error: An organization slug is required (provide with --org)

Add --log-level=[info|debug] or export SENTRY_LOG_LEVEL=[info|debug] to see more output.
Please attach the full debug log to all bug reports.
```

The issue that we are encountering is that even if we are to run the `upload-proguard` subcommand with a seemingly correctly configured invocation, it still provides no output and seemingly does nothing:

```
node_modules/@sentry/cli/bin/sentry-cli --auth-token replace_with_actual_auth_token upload-proguard --log-level=debug --require-one --org replace_with_actual_org --project replace_with_actual_project --write-properties path/to/actual/proguard/file
```

> Please note actual values have been edited out aboe, as this is a public repo.

Encountering this issue is preventing us from uploading any Android Proguard mappings at all, as using the Sentry Gradle plugin is not an option for us due to the way our project is configured.

## Our environment

Issue is reproducible on multiple machines. The environment is the following:

- macOS Big Sur 11.6.1
- `zsh` or `bash` shell

## How to preproduce using this repository

This example repo also reproduces the issue. Just run:

```
node_modules/@sentry/cli/bin/sentry-cli upload-proguard
```
