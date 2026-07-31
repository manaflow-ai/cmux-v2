# Browser binary licensing

This repository is a distribution endpoint, not the product development
repository. Its original material and independently authored cmux portions of
the browser are distributed under GPL-3.0-or-later. Current browser releases
also contain modified Helium material licensed under GPL-3.0-only, so the
combined GPL-covered browser work is distributed under GPL-3.0-only.
Compatible third-party components retain their respective licenses. See
[`LICENSE`](LICENSE) for the standard terms and
[`COPYRIGHT.md`](COPYRIGHT.md) for the copyright and scope notice.

## Current nightly builds

The current cmux Browser build contains:

- independently authored cmux code distributed under GPL-3.0-or-later;
- modified adaptations of Helium code distributed under GPL-3.0-only;
- Chromium code and resources under BSD and other third-party licenses;
- Ghostty and bundled dependencies under their respective licenses; and
- optional bundled extensions and resources under their respective licenses.

Accordingly, each current browser nightly, as a combined GPL-covered work, is
distributed under GPL-3.0-only. This narrower license for the combined work
does not change the GPL-3.0-or-later grant on independently authored cmux
portions or the separate licenses of compatible third-party components. Each
release must include:

1. `cmux-browser-source-<version>.tar.zst`, the exact corresponding source and
   build/install scripts for that binary;
2. `THIRD_PARTY_NOTICES.html` and the machine-readable notice inventory;
3. the full GPL license and every required bundled-component license; and
4. SHA-256 checksums covering the installers, updater archives, source, and
   notice bundle.

The corresponding source must remain available from the same release page at
no charge for as long as the object code is offered there.

## GPL grant

The GPL rights granted for repository revisions and browser releases are
irrevocable as long as recipients comply with the license. A future,
independently authored project may use different terms only if it contains no
incompatible GPL-derived or outside-contributor material; that cannot revoke
rights already granted for cmux-v2 releases.

This document describes the release policy; it is not a substitute for the
license files accompanying a particular asset.
