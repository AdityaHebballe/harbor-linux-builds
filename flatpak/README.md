# Flatpak packaging

This directory is maintained by the Linux packaging repository. The workflow overlays
it onto an exact Harbor checkout, so it remains the Flatpak source of truth even if
Harbor removes its own `flatpak/` directory. `source-ref.txt` records the Harbor
commit used to generate the currently committed dependency sources.
`tauri.flatpak.conf.json` is the downstream Tauri override that supplies the Flatpak
application ID and disables native bundle/external-binary handling.

Harbor is built as `site.harbor.Harbor` against the pinned GNOME 49 SDK. mpv is
built in the sandbox, FFmpeg tools come from the SDK and use the codecs supplied
through the matching platform runtime, and yt-dlp is installed at a digest-pinned
version. No host multimedia tools are visible to the application.

Build locally with the runtimes listed in the manifest installed:

```sh
flatpak-builder --user --force-clean --default-branch=stable --state-dir=.flatpak-work/state --repo=.flatpak-work/repo .flatpak-work/build flatpak/site.harbor.Harbor.yml
flatpak build-bundle .flatpak-work/repo Harbor.flatpak site.harbor.Harbor stable
flatpak install --user Harbor.flatpak
```

Stable and beta use the same application ID on separate Flatpak branches. Replace
`stable` with `beta` in both build commands to create the beta channel, then run it
with `flatpak run site.harbor.Harbor//beta`.

The package intentionally grants no home or host filesystem access. File and
folder choices are made through the desktop portal. Runtime smoke tests should
cover Wayland and X11, AMD and NVIDIA, WebKit rendering, mpv hardware decode,
FFmpeg casting/transcoding, trailers, torrents, localhost playback, audio, deep
links, tray integration, Discord IPC, and portal-selected media/download paths.

To audit the sandbox, run `flatpak run --command=sh site.harbor.Harbor` and verify
that `/usr/bin/mpv`, `/usr/bin/ffmpeg`, and `/usr/bin/yt-dlp` do not exist; the
packaged commands must resolve under `/app/bin`.

## Updating JavaScript or Rust dependencies

The packaging workflow refreshes release metadata and pinned dependency sources for
each exact Harbor commit, then commits that update here. To refresh them locally:

```sh
flatpak/update-flatpak.sh
```

The script uses a pinned revision of
[`flatpak-builder-tools`](https://github.com/flatpak/flatpak-builder-tools).
Set `RELEASE_DATE=YYYY-MM-DD` when preparing a release for a date other than
today. Commit its output before running the Flatpak workflow.

The script also updates the pnpm archive URL and SHA-256 when `packageManager`
changes. Keep `--offline`, `--frozen-lockfile`, and `CARGO_NET_OFFLINE=true`;
removing them would hide a missing generated source until CI or a Flathub build.
