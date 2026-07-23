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

## Beta builds

`Build Harbor Linux Beta` is a separate manual workflow for upstream
`beta-branch` (or a supplied beta commit). It creates a release tagged as
`beta-v<version>-<commit>` and updates the AUR package
[`harbor-stremio-beta-bin`](https://aur.archlinux.org/packages/harbor-stremio-beta-bin).

The beta package conflicts with `harbor-stremio-bin`: both contain the same
Harbor executable and desktop integration, so they cannot be installed side by
side. It is intentionally manual-only for now; a later decision can add a
per-commit or version-change trigger without changing the package layout.

## Trust Model

These binaries are not official Harbor upstream binaries. They are built by this
repository's GitHub Actions workflow from upstream Harbor release tags.
