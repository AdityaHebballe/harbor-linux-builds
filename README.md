# Harbor Linux Builds

Unofficial Linux release builds for [Harbor](https://github.com/harborstremio/harbor).

This repository exists so Arch/AUR packaging can consume stable Linux binary
artifacts while upstream does not attach Linux bundles to GitHub Releases.

The workflow builds Harbor from the exact upstream tag, then publishes the Linux
bundle files to this repository's matching release tag.

## Usage

Run the `Build Harbor Linux Release` workflow manually with a tag such as:

```text
v0.9.12
```

If no tag is provided, the workflow uses the latest upstream Harbor release.

The scheduled run checks for a new upstream release and exits if this repository
already has a release for that tag.

## Trust Model

These binaries are not official Harbor upstream binaries. They are built by this
repository's GitHub Actions workflow from upstream Harbor release tags.

