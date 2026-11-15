# Fork notes

This repository is a fork of
[QuantumEntangledAndy/neolink](https://github.com/QuantumEntangledAndy/neolink).
The `penguincam` branch carries a short series of commits on top of upstream
`master`. The README describes neolink itself. This file covers only the fork.

## What this fork adds

| Area | Change |
|---|---|
| RTSP stability | No buffer pool leak. Bounded waits in the client lifecycle. One shared media per mount path, recovered or evicted when the camera stream ends, on GStreamer 1.22 and later. Motion watcher tasks and frame pushers end with their owner. |
| RTSP timing | PTS stays monotonic and follows the camera's own timestamps, with tests for clock wrap, restart and frame rate change. |
| RTSP audio | A per camera `audio_codec` key serves AAC, G.711 mu-law, L16 or no audio. |
| Alarms | `BcCamera::listen_on_alarms` forwards each raw `AlarmEvent`, AI type included. The alarm subscription starts before the request, so no early alarm is lost. |
| Core fixes | The poller ends on a clean close. Each open discovery request gets its own tid. `update_time = false` never writes the camera clock. |
| Tests | A `test-util` feature in `neolink_core` with an in-memory fake camera. The workspace uses Cargo resolver 2. |
| CI | The retired macos-12 runner is gone and releases use action-gh-release v2. |

Each change is one commit with its reason in the message. Three of the RTSP
fixes were written by the maintainer of the fork at
[github.com/alexbahder/neolink](https://github.com/alexbahder/neolink). They
are carried here with him as author.

## How it tracks upstream

- The series sits on upstream `master` at commit `6e05e78`.
- When upstream moves, the series is rebased onto the new upstream `master`.
  It is never merged into it.
- Changes that suit upstream are offered there as pull requests. A change
  that upstream merges leaves the series at the next rebase.
- Releases of this fork are tagged on the `penguincam` branch.

## Contributing

Write access stays with the maintainer. Work from your own fork named
`neolink-contrib` and open a pull request against the `penguincam` branch.
Commits are signed.

## Licence

The `LICENSE` file holds the text of the GNU Affero General Public License
version 3. `Cargo.toml`, `crates/core/Cargo.toml` and
`crates/decoder/Cargo.toml` declare `license = "AGPL-3.0-or-later"`.
`crates/mailnoti/Cargo.toml` and `crates/pushnoti/Cargo.toml` declare no
licence. The README says neolink is released under
the GNU Affero General Public License v3. The changes in this fork are
offered under the same terms. The copyright in upstream code stays with its
authors.
