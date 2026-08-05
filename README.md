# cmux Browser nightlies

This repository is the public distribution endpoint for cmux Browser nightly
builds. Product development happens in a separate private repository.

## Downloads

### Linux x64 nightly

**[Open the cmux Browser download page for Linux](https://cmux.com/linux)**

Recommended first install:

**[Download the Linux x64 per-user installer (.run)](https://cmux.com/api/download/browser-nightly/linux-x64/run)**

This is the recommended first-install download for a Linux desktop. It installs
below `~/.local` without root access so cmux Browser can apply future signed
updates atomically.

Other Linux nightly files:

- Debian/Ubuntu package:
  [download `cmux-linux-x64.deb`](https://cmux.com/api/download/browser-nightly/linux-x64/deb).
  This root-owned installation must be updated through the package manager.
- In-app updater payload only, **not a first installer**:
  [`cmux-linux-x64.zip`](https://cmux.com/api/download/browser-nightly/linux-x64/zip).

The `cmux.com` links are the stable download contract. The server verifies the
P-256-signed update feed, selects the requested platform and architecture, and
redirects only to an allowlisted asset in this public repository. Versioned
binaries live on immutable `nightly-<version>` releases, so do not construct a
`releases/download/nightly/<binary>` URL; moving-channel binary assets are not
part of the durable contract.

### Platform availability

| Platform | Status | Supported download |
| --- | --- | --- |
| Linux (x64) | Available | [Linux download page](https://cmux.com/linux) |
| macOS (Universal 2) | Unavailable | No download until the signed feed contains both `mac-arm64` and `mac-x64` and the notarized universal assets pass fresh-install checks |
| Windows (x64) | Unavailable | No download until the signed feed contains `windows-x64` and the Authenticode-signed assets pass fresh-install checks |

`update.json` is the signed manifest consumed by the browser. It is published
only after every package, checksum, notice bundle, and corresponding-source
artifact for each enabled platform is available. A platform does not become
supported merely because a filename is documented here: its installer must be
present on the immutable release and its update payload must be present in the
signed manifest.

Until a platform is enabled by the signed public feed, there is no supported
download for that platform. Do not obtain builds from Actions artifacts or
private source-repository releases: those are not the public update channel.

## Update authenticity

Every browser build embeds the P-256 public key in
[`update-public-key.pem`](update-public-key.pem). The browser checks the
manifest signature, selected platform, version, byte length, and SHA-256
digest before staging an update. macOS and Windows releases additionally
require their native platform signatures.

Public-key fingerprint:

```text
SHA-256 8feeefcadd6c55cfeb3dc3aeb52ca95649d914cc1430c9c798c9567374b6f657
```

## Corresponding source and licensing

Each immutable binary release has its exact
`cmux-browser-source-<version>.tar.zst`, source manifest, build/install scripts,
GPL text, notices, checksums, and provenance on the same release page. Browse
the [public immutable release history](https://github.com/manaflow-ai/cmux-v2/releases)
to find the version shown by an installed browser. Long-lived component source
archives, the Chromium source closure, and their inventories are retained on
the [source-snapshots release](https://github.com/manaflow-ai/cmux-v2/releases/tag/source-snapshots).

Original material in this repository and independently authored cmux portions
of the browser are distributed under GPL-3.0-or-later. Current cmux Browser
releases combine that material with modified Helium material licensed under
GPL-3.0-only, so the combined GPL-covered browser work is distributed under
GPL-3.0-only. Compatible third-party components retain their respective
licenses. See [`LICENSE`](LICENSE) and the [`COPYRIGHT.md`](COPYRIGHT.md)
copyright and scope notice.

See [`BINARY-LICENSING.md`](BINARY-LICENSING.md) for the corresponding-source
contract and [`LICENSE`](LICENSE) for the complete GPL text.
