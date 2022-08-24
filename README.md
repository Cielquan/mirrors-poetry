DEPRECATED poetry mirror
========================

Mirror of poetry for pre-commit. Inspired by mirror repos of https://github.com/pre-commit.

This mirror will be archived when https://github.com/python-poetry/poetry/pull/2511 is merged.

**EDIT:**
**The PR was merged and was released with the 1.2.0b1 pre-release. As of this this repository is deprecated.**
**Currently versions 1.1.15 and 1.2.0rc1 are the latest releases supported here.**
**New releases of 1.1.x are only supported on request via issue.**

For pre-commit: see https://github.com/pre-commit/pre-commit
For poetry: see https://github.com/python-poetry/poetry

### Using poetry with pre-commit:

Add this to your `.pre-commit-config.yaml`

```yaml
-   repo: https://github.com/cielquan/mirrors-poetry
    rev: ''  # Use the sha / tag you want to point at
    hooks:
    -   id: poetry-check
```

### poetry-check

The `poetry-check` hook calls the `poetry check` command
to make sure the poetry configuration does not get committed in a broken state.

#### Arguments

The hook takes the same arguments as the poetry command.
For more information see the https://python-poetry.org/docs/cli/#check.


### poetry-lock

The `poetry-lock` hook calls the `poetry lock` command
to make sure the lock file is up-to-date when committing changes.

#### Arguments

The hook takes the same arguments as the poetry command.
For more information see the https://python-poetry.org/docs/cli/#lock.


### poetry-export

The `poetry-export` hook calls the `poetry export` command
to sync your `requirements.txt` file with your current dependencies.

**NOTE**: It is recommended to run the `poetry-lock` hook prior to this one.

#### Arguments

The hook takes the same arguments as the poetry command.
For more information see the https://python-poetry.org/docs/cli/#export.

`args: ["-f", "requirements.txt", "-o", "requirements.txt"]` are the default arguments
which will create/update the requirements.txt file in the current working directory.

For output to the console change the arguments and add `verbose: true` to `poetry-export`
in your `.pre-commit-config.yaml` file like so:

```yaml
hooks:
  - id: poetry-export
    args: ["-f", "requirements.txt"]
    verbose: true
```

Or to put the `dev` dependencies into the `requirements.txt` also use this:

```yaml
hooks:
  - id: poetry-export
    args: ["--dev", "-f", "requirements.txt", "-o", "requirements.txt"]
```

