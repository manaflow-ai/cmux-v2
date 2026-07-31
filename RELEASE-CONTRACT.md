# Nightly release contract

The `nightly` tag is a moving prerelease channel. Platforms may be enabled
incrementally, but publication is transactional from the updater's point of
view for every enabled platform.

## Required assets

Every publication requires:

- `cmux-browser-source-<version>.tar.zst`
- `THIRD_PARTY_NOTICES.html`
- `third-party-notices.spdx.json`
- `SHA256SUMS`
- `provenance.intoto.jsonl`
- `update.json`

It also requires the complete asset group for each enabled platform:

- macOS: `cmux-macos-arm64.dmg` and `cmux-macos-arm64.zip`;
- Windows: `cmux-windows-x64-installer.exe` and
  `cmux-windows-x64.zip`; and
- Linux: `cmux-linux-x64-installer.run`, `cmux-linux-x64.deb`, and
  `cmux-linux-x64.zip`.

The signed manifest must contain exactly the enabled updater platforms. A
platform must not be advertised as available until its complete asset group
has passed the checks below and is present on the public release.

## Publication order

1. Build from one reviewed cmux Browser commit and record it in provenance.
2. Verify native signatures and notarization where applicable.
3. Exercise fresh-install launch checks on every enabled operating system.
4. Exercise an older nightly updating to the candidate on every enabled
   operating system, using the per-user Linux installation rather than the
   root-owned `.deb`.
5. Upload packages, corresponding source, notices, checksums, and provenance.
6. Confirm every uploaded asset is anonymously downloadable and matches its
   recorded digest.
7. Sign and upload `update.json` last.
8. Confirm the manifest and every URL in its decoded payload are anonymously
   downloadable before updating website availability.

If any step fails, retain the previous `update.json`; clients will continue to
use the last complete nightly.

## Versioning

Nightly versions retain the pinned Chromium major, minor, and build numbers and
use a monotonically increasing fourth component. A release must never publish
a version less than or equal to the version embedded in its predecessor.
