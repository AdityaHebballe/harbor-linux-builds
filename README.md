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

Stable releases include Debian, RPM, AppImage, and Flatpak bundle artifacts.
The Flatpak build is separate from the core release/AUR job, so a Flatpak-only
failure does not prevent the other three formats from publishing.

## Beta builds

`Build Harbor Linux Beta` is a separate manual workflow for upstream
`beta-branch` (or a supplied beta commit). It creates a release tagged as
`beta-v<version>-<commit>` and updates the AUR package
[`harbor-stremio-beta-bin`](https://aur.archlinux.org/packages/harbor-stremio-beta-bin).
Beta builds are GitHub pre-releases, so the stable release remains the
repository's single GitHub `Latest` release while the newest pre-release is the
latest beta build.

The beta package conflicts with `harbor-stremio-bin`: both contain the same
Harbor executable and desktop integration, so they cannot be installed side by
side. It runs every five hours and compares the current beta commit with the
commit encoded in an existing beta release tag. If that exact commit was
already published, it exits without rebuilding. Beta releases use the same
four artifact formats and the same non-blocking Flatpak job.

The beta builder also applies narrowly scoped compatibility fixes for upstream
beta metadata when needed, including its current missing face-asset fetch
script. The models themselves are already committed in that branch.

## Trust Model

These binaries are not official Harbor upstream binaries. They are built by this
repository's GitHub Actions workflow from upstream Harbor release tags.
