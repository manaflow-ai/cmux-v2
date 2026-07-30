# Nightly release contract

The `nightly` tag is a moving prerelease channel. Publication is transactional
from the updater's point of view.

## Required assets

- `cmux-macos-arm64.dmg`
- `cmux-macos-arm64.zip`
- `cmux-windows-x64-installer.exe`
- `cmux-windows-x64.zip`
- `cmux-linux-x64.deb`
- `cmux-linux-x64.zip`
- `cmux-browser-source-<version>.tar.zst`
- `THIRD_PARTY_NOTICES.html`
- `third-party-notices.spdx.json`
- `SHA256SUMS`
- `provenance.intoto.jsonl`
- `update.json`

## Publication order

1. Build from one reviewed cmux Browser commit and record it in provenance.
2. Verify native signatures and notarization where applicable.
3. Exercise fresh-install launch checks on all three operating systems.
4. Exercise an older nightly updating to the candidate on all three systems.
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
