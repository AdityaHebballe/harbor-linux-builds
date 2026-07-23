# Harbor for Linux

Unofficial Linux builds of [Harbor](https://github.com/harborstremio/harbor), built from its upstream source tags by GitHub Actions.

<p align="center">
  <a href="https://github.com/AdityaHebballe/harbor-linux-builds/releases/latest"><strong>Download stable</strong></a>
  ·
  <a href="https://github.com/AdityaHebballe/harbor-linux-builds/releases"><strong>Browse beta builds</strong></a>
  ·
  <a href="https://github.com/harborstremio/harbor"><strong>Harbor upstream</strong></a>
</p>

> **x86_64 only.** Choose the package that fits your distribution below. Every stable download is on the [latest release](https://github.com/AdityaHebballe/harbor-linux-builds/releases/latest).

<table>
  <tr>
    <td width="50%" valign="top">
      <h3>Arch Linux</h3>
      <p>Install from the AUR. Updates arrive through your usual AUR helper.</p>
      <p><a href="https://aur.archlinux.org/packages/harbor-stremio-bin"><strong>Open harbor-stremio-bin on AUR →</strong></a></p>
      <pre><code>paru -S harbor-stremio-bin</code></pre>
      <p><sub>Replace <code>paru</code> with <code>yay</code> if that is your helper.</sub></p>
    </td>
    <td width="50%" valign="top">
      <h3>Debian, Ubuntu &amp; Mint</h3>
      <p><a href="https://github.com/AdityaHebballe/harbor-linux-builds/releases/latest"><strong>Download the latest .deb →</strong></a></p>
      <pre><code>cd ~/Downloads
sudo apt install ./Harbor_*.deb</code></pre>
    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">
      <h3>Fedora &amp; openSUSE</h3>
      <p><a href="https://github.com/AdityaHebballe/harbor-linux-builds/releases/latest"><strong>Download the latest .rpm →</strong></a></p>
      <pre><code># Fedora
sudo dnf install ./Harbor-*.rpm

# openSUSE
sudo zypper install ./Harbor-*.rpm</code></pre>
    </td>
    <td width="50%" valign="top">
      <h3>Any desktop Linux</h3>
      <p><a href="https://github.com/AdityaHebballe/harbor-linux-builds/releases/latest"><strong>Download the latest AppImage →</strong></a></p>
      <pre><code>cd ~/Downloads
chmod +x Harbor_*.AppImage
./Harbor_*.AppImage</code></pre>
    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">
      <h3>Flatpak</h3>
      <p><a href="https://github.com/AdityaHebballe/harbor-linux-builds/releases/latest"><strong>Download the latest .flatpak →</strong></a></p>
      <pre><code>cd ~/Downloads
flatpak install --user ./Harbor_*.flatpak</code></pre>
    </td>
    <td width="50%" valign="top">
      <h3>Verify a download</h3>
      <p>Each release includes a SHA-256 checksum file for the core package assets.</p>
      <p><a href="https://github.com/AdityaHebballe/harbor-linux-builds/releases/latest"><strong>Get SHA256SUMS →</strong></a></p>
      <pre><code>sha256sum -c SHA256SUMS-*.txt</code></pre>
    </td>
  </tr>
</table>

## Beta channel

Beta packages follow Harbor's `beta-branch` and are published as GitHub pre-releases every five hours when that branch changes.

- [Browse beta downloads](https://github.com/AdityaHebballe/harbor-linux-builds/releases)
- Arch Linux: [`harbor-stremio-beta-bin`](https://aur.archlinux.org/packages/harbor-stremio-beta-bin)

```bash
paru -S harbor-stremio-beta-bin
```

The stable and beta AUR packages conflict: they install the same Harbor application, so install one channel at a time.

## How it works

Stable releases track upstream Harbor release tags. Beta releases track an exact commit from `beta-branch`. New releases provide `.deb`, `.rpm`, AppImage, and Flatpak bundles; Flatpak is built separately so its failure never blocks the other packages or the AUR update.

These are community-maintained builds, not binaries published by the upstream Harbor project. The workflow and exact upstream source ref for each build are visible in the [Actions tab](https://github.com/AdityaHebballe/harbor-linux-builds/actions).
