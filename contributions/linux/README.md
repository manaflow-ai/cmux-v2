# Proposed Linux repair patches

The Linux nightly can flicker or crash when terminals are added/closed, fail to
create new terminals after an update, and miss clipboard/IME input. This patch
set repairs those paths in the published corresponding source and includes
regression coverage. It also fixes device scaling, adds basic appearance
controls, and avoids an unwanted browser tab during workspace projection.

This is a **draft contribution against the published source snapshot**, offered
here because this public repository is the distribution/issue endpoint and the
browser development repository is private. Maintainers can import or split the
source commits in their development repository. These files do not modify the
release feed or publish a binary.

## Source and application

- Published source revision: `dd7984e7ea68ee42768feebe3691b7b7ffdca6e6`
  (the corresponding source for binary `151.0.7922.64`).
- Chromium baseline/local build version: `151.0.7922.34`.
- [Source import](https://github.com/Steve-Strange/cmux-v2/tree/a64f83a2f61fb8c1c8cdb68e01acb87728c0fbe6);
  [repaired source](https://github.com/Steve-Strange/cmux-v2/tree/98fa41c670f7923a2cfcec9a623b5acb8c8445a2).
- [Detailed implementation and reproduction](https://github.com/Steve-Strange/cmux-v2/blob/98fa41c670f7923a2cfcec9a623b5acb8c8445a2/docs/linux-repair.md).
- [`repairs.patch`](repairs.patch) is a four-commit `git format-patch` mailbox.
  Apply it **in the published browser source tree**, using:

```sh
git am /absolute/path/to/contributions/linux/repairs.patch
```

The four commits preserve running backend executables during upgrades; repair
terminal lifecycle, desktop input, scaling, settings and startup projection;
protect marked local builds from being overwritten and package appearance
presets; and document validation. The complete mailbox was applied one commit
at a time to the imported base and reproduced the exact repaired source tree.
The source archive's licensing and provenance are preserved.

## Tracked problems

- Renderer retry/lifecycle failures: existing [#15](https://github.com/manaflow-ai/cmux-v2/issues/15) and [#16](https://github.com/manaflow-ai/cmux-v2/issues/16).
- Update removes executables still used by daemons: [#18](https://github.com/manaflow-ai/cmux-v2/issues/18).
- Fcitx/Sogou composition and commits: [#19](https://github.com/manaflow-ai/cmux-v2/issues/19).
- Clipboard/PRIMARY and Control-modified bindings: [#20](https://github.com/manaflow-ai/cmux-v2/issues/20).

## Validation and limits

[`validation.json`](validation.json) contains a sanitized summary. Publication
checks passed all 28 host tests, the user-installer suite, and mailbox application.
The 24 modified frontend source files match the locally built/validated tree.
Recorded Linux tests include 30 lifecycle cycles plus 300 seconds of output,
real EGL host teardown, Unicode/multiline clipboard/PRIMARY, actual Sogou `你好`
input, settings persistence, and GUI restart without placeholder browser tabs.
The 300-second lifecycle run predates the final input changes; the final package
and installed-input runs are separately identified in the summary.

Validation is on Ubuntu 24.04.3 KDE/X11, including 1.75 scale and isolated
Qt/GTK/Mesa runs. Windows, macOS and Wayland are untested. Some files are shared
with other platforms and require maintainer build/regression checks. Retained
old installation directories currently have no automatic later garbage collection.
GUI restart tests kept backend/PTY processes alive: machine reboot recovery,
tmux/SSH resurrection, AI conversation restore and completion notifications
are outside this contribution. No user terminal/profile data is included.
