# cmux Browser nightlies

This repository is the public distribution endpoint for cmux Browser nightly
builds. Product development happens in a separate private repository.

## Downloads

The moving [`nightly`](https://github.com/manaflow-ai/cmux-v2/releases/tag/nightly)
release will contain:

| Platform | First install | In-app update payload |
| --- | --- | --- |
| macOS (Apple silicon) | `cmux-macos-arm64.dmg` | `cmux-macos-arm64.zip` |
| Windows (x64) | `cmux-windows-x64-installer.exe` | `cmux-windows-x64.zip` |
| Linux (x64) | `cmux-linux-x64-installer.run` | `cmux-linux-x64.zip` |

The Linux website installer places the browser below `~/.local` without root
access, which lets the in-app updater replace it atomically. A
`cmux-linux-x64.deb` is also published for package-manager-managed systems;
because that installation is root-owned, update it through the package manager
rather than the in-app updater.

`update.json` is the signed manifest consumed by the browser. It is published
only after every package, checksum, notice bundle, and corresponding-source
artifact referenced by that nightly is available.

Until the first complete release is present, there is no supported download.
Do not obtain builds from Actions artifacts or private source-repository
releases: those are not the public update channel.

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

## Licensing

Original material in this repository and the combined cmux Browser work are
distributed under GPL-3.0-or-later; see [`LICENSE`](LICENSE) and the
[`COPYRIGHT.md`](COPYRIGHT.md) copyright and scope notice.

Every release includes its exact corresponding source, build/install scripts,
GPL text, and third-party notices. See
[`BINARY-LICENSING.md`](BINARY-LICENSING.md) for the release contract.
