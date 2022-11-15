poetry pre-commit mirror
========================

The branching model of `poetry` and the latest release detection of `pre-commit` are unfortunately incompatible.
This repo solves the issue, by releasing new poetry releases itself on the default branch so that `pre-commit autoupdate` can detect it and corretly upgrade.

### How to use:

For supported hooks see: https://python-poetry.org/docs/pre-commit-hooks/

Add this to your `.pre-commit-config.yaml`

```yaml
-   repo: https://github.com/cielquan/mirrors-poetry
    rev: ''  # Use the sha / tag you want to point at
    hooks:
    -   id: poetry-check
```

### How it works

This repo has a Github Actions workflow which runs ever night and checks if there is a new release of poetry. It compares the last sorted git tag with the current version of this repo. If a newer version is detected, this repo's pre-commit-hooks config and versions are updated, then the changes are released with the new version. **Only a new tag is created and no new Github Release.**

`pre-commit` checks the default branch for the latest created tag and takes it as the latest release. Therefore only the latest major/minor releases are supported and patch releases for older major/minor releases are ignored (by this repo). Should you need such a patch release you need to directly use the `poetry` repo in your pre-commit config with the needed version.

**This repo only tries to solve the issue of running `pre-commit autoupdate` for `poetry`.**

See for more information: https://github.com/python-poetry/poetry/discussions/7018

### Links

Inspired by mirror repos of https://github.com/pre-commit.
For pre-commit: see https://github.com/pre-commit/pre-commit
For poetry: see https://github.com/python-poetry/poetry
