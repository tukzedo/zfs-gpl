<!-- markdownlint-disable MD007 -- Unordered list indentation -->
<!-- markdownlint-disable MD010 -- No hard tabs -->
<!-- markdownlint-disable MD041 -- First line in a file should be a top-level heading -->

<!-- TOC ignore:true -->
# Project backlog

<!-- TOC ignore:true -->
## Table of contents

<!-- TOC -->

- [Introduction](#introduction)
- [Issues](#issues)
- [Old format](#old-format)
	- [Bugs](#bugs)
	- [Features and enhancements](#features-and-enhancements)
	- [Done](#done)
		- [Done - Bugs](#done---bugs)
		- [Done - Features and enhancements](#done---features-and-enhancements)
	- [Deferred](#deferred)
	- [Canceled](#canceled)
- [Template](#template)

<!-- /TOC -->

## Introduction

Going forward, new issues in the new template at the bottom of this file, will go in the '## New format' section only. No more status emojis. Refer to '## Reference' for sort order. Issues in the old format (with status emojis) won't be refactored, but will continue to be worked until moved to closed, canceled, or deferred sections, and emojis updated. (Eventually this will all be moved to nano-git-db anyway. This new template is an intermediate effort to make issues going forward more structured and importable.)

This is a product backlog just for the pre-v1.0.0 release. After that, bugs, features, and enhancements will be managed in GitHub Issues. Companion: [`design.md`](design.md). Process: [`../cleanroom.md`](../cleanroom.md).

## Issues

- CICD reset: standard flags
	- ID: 2026102416291700
	- Type: Task
	- Status: Queued
	- Priority: High
	- Opened: 20261024-162917
	- Opened by: CICD reset
	- Requirements:
		- There's no pipeline yet. Add `cicd.bash` with the shared flags, from `--quick` and `--long` to `--backlog-run-quick` and `--merge-gate`, plus `--quiet` and `--message`.
		- Format check, clippy with `-D warnings`, the tests, release builds, and cross-builds in the default run, which stays under about an hour.
		- `--merge-gate` from a pre-push hook on `main`, skipped when a push changes only docs. Nothing gates a push to a feature branch.
		- A backlog run never dogfoods, publishes, commits, or pushes.
		- Sweeping override, 2026-10-24: this supersedes any earlier decision on this project that conflicts with it.
		- Supersedes the old-format "CI/CD pipeline" and Phase 0 "CI: build, test, fmt, clippy" items, for everything but the pre-commit hook.
		- Supersedes the cross-build cadence in the private notes, which cross-builds only after big changes or every fifth Linux build.

- CICD reset: containers
	- ID: 2026102416291701
	- Type: Task
	- Status: Queued
	- Priority: High
	- Opened: 20261024-162917
	- Opened by: CICD reset
	- Requirements:
		- Build and test in a container from a pinned recipe in the repo, with the Rust toolchain pinned to an exact version. Fall back to the host in one line when docker is missing, and take `--no-container`.
		- Sweeping override, 2026-10-24: this supersedes any earlier decision on this project that conflicts with it.

- CICD reset: other hosts and VMs
	- ID: 2026102416291702
	- Type: Task
	- Status: Queued
	- Priority: High
	- Opened: 20261024-162917
	- Opened by: CICD reset
	- Requirements:
		- Run the tests for each target that's built: Windows on `b29w`, FreeBSD on its VM, and Linux arm64 on its VM, through the shared host lock and the VM state helper.
		- A box that isn't there is a SKIP in its step and in the summary, never a failure. `--no-remote` skips them all.
		- Each box gets a per-project work folder under its temp root.
		- Sweeping override, 2026-10-24: this supersedes any earlier decision on this project that conflicts with it.

- CICD reset: Zig cache
	- ID: 2026102416291703
	- Type: Task
	- Status: Queued
	- Priority: High
	- Opened: 20261024-162917
	- Opened by: CICD reset
	- Requirements:
		- The arm64 cross-builds are planned through `cargo zigbuild`. Keep the project's Zig caches between runs, and empty a whole one at the end of a run when it's over 2 GB or was filled by another Zig version.
		- The container mounts a volume of its own for Zig's global cache, under the same rule. The shared one on the host is never touched.
		- Sweeping override, 2026-10-24: this supersedes any earlier decision on this project that conflicts with it.

- CICD reset: container cleanup
	- ID: 2026102416291704
	- Type: Task
	- Status: Queued
	- Priority: High
	- Opened: 20261024-162917
	- Opened by: CICD reset
	- Requirements:
		- Label, name, and `--rm` every container, and remove the run's containers, the project's stale images, and old build cache by label at the end of a run, per the shared CICD rules.
		- Sweeping override, 2026-10-24: this supersedes any earlier decision on this project that conflicts with it.

- CICD reset: CPU and priority
	- ID: 2026102416291705
	- Type: Task
	- Status: Queued
	- Priority: High
	- Opened: 20261024-162917
	- Opened by: CICD reset
	- Requirements:
		- Work out one job count from the CPU count and load, and pass it to cargo, the test threads, and the container's CPU cap. Run at low priority, and at a quarter of the CPUs for the sanitizer and Miri runs.
		- Sweeping override, 2026-10-24: this supersedes any earlier decision on this project that conflicts with it.

- CICD reset: step output
	- ID: 2026102416291706
	- Type: Task
	- Status: Queued
	- Priority: High
	- Opened: 20261024-162917
	- Opened by: CICD reset
	- Requirements:
		- Use the numbered Starting and PASS or FAIL step lines with the section rule, list turned-off steps first, and end with a blank line.
		- Sweeping override, 2026-10-24: this supersedes any earlier decision on this project that conflicts with it.

- CICD reset: a test for every Done item
	- ID: 2026102416291707
	- Type: Task
	- Status: Queued
	- Priority: High
	- Opened: 20261024-162917
	- Opened by: CICD reset
	- Requirements:
		- Each Done item names its test, or says in a few words why it has none.
		- Sweeping override, 2026-10-24: this supersedes any earlier decision on this project that conflicts with it.

- CICD reset: test IDs
	- ID: 2026102416291708
	- Type: Task
	- Status: Queued
	- Priority: High
	- Opened: 20261024-162917
	- Opened by: CICD reset
	- Requirements:
		- Give each test a base 32 minute ID from its first commit, and print one PASS, FAIL, or SKIP line per test with it.
		- Sweeping override, 2026-10-24: this supersedes any earlier decision on this project that conflicts with it.

- Run on the last Core 2 Duo, and AMD CPUs from that era.
	- ID: 2026101301161891
	- Type: Enhancement
	- Status: Queued
	- Needs external testing: Yes, on an old CPU or an emulated one.
	- Priority [Feature|Enhancement] | Severity [Bug]: Avg
	- Opened: 20261013-011618
	- Opened by: JC
	- Target OS: Linux, Windows and FreeBSD on x86_64, where this project builds them. Macs that old can't run a current macOS anyway.
	- Requirements [Feature]:
		- Release builds run on the last Core 2 Duo (Penryn, 2008), and on AMD Phenom II and Athlon II, if that's reasonably doable.
			- Penryn has SSSE3 and SSE4.1 but no POPCNT. The AMD ones have POPCNT but no SSSE3. So the shared floor is plain x86-64, also called x86-64-v1.
		- If that isn't doable, the floor is the first Core i3/i5/i7 (Nehalem, 2008), which is x86-64-v2. AMD's first chip at that level is Bulldozer, 2011.
		- Faster code for newer CPUs is still fine, but it's picked at run time by a CPU feature test, never by the build target.
		- Tests run the release build on an emulated Penryn and Phenom II, through Intel SDE or QEMU's `-cpu Penryn` and `-cpu phenom`.
	- Progress log:
		- 20261013: Rust builds for plain x86-64 by default, and nothing here sets `target-cpu`. Keep `target-cpu=native` out of the release profile. Checksum (fletcher4, SHA-256) and compression fast paths go through `is_x86_feature_detected!`.

- CICD reset: temp files and safe removal
	- ID: 2026102416291709
	- Type: Task
	- Status: Queued
	- Priority: Avg
	- Opened: 20261024-162917
	- Opened by: CICD reset
	- Requirements:
		- Put each run's temp folder under the shared layout, with `TMPDIR` pointed there, a cleanup trap, and pruning of the project's own stale runs. Remove through a copy of the shared guard.
		- Sweeping override, 2026-10-24: this supersedes any earlier decision on this project that conflicts with it.

- CICD reset: version line
	- ID: 2026102416291710
	- Type: Task
	- Status: Queued
	- Priority: Avg
	- Opened: 20261024-162917
	- Opened by: CICD reset
	- Requirements:
		- `zgpl` has no `--version`. Add one with the version from `Cargo.toml`, the build number from the commit time, and the date on a non-release build.
		- Sweeping override, 2026-10-24: this supersedes any earlier decision on this project that conflicts with it.

- CICD reset: macOS runner
	- ID: 2026102416291711
	- Type: Task
	- Status: Queued
	- Priority: Avg
	- Opened: 20261024-162917
	- Opened by: CICD reset
	- Requirements:
		- macOS builds wait on a Mac. Once the repo is public, build and run the tests on GitHub's free arm64 macOS runner, and smoke-test `zgpl` there.
		- Sweeping override, 2026-10-24: this supersedes any earlier decision on this project that conflicts with it.
		- Supersedes "macOS is deferred" in the cross-build cadence in the private notes.

- CICD reset: CICD process gaps
	- ID: 2026102416291712
	- Type: Task
	- Status: Queued
	- Priority: Avg
	- Opened: 20261024-162917
	- Opened by: CICD reset
	- Requirements:
		- The Rust leak checks: AddressSanitizer and LeakSanitizer on a pinned nightly, Miri, and the clippy `mem_forget` and `undocumented_unsafe_blocks` lints.
		- `cargo deny` advisories, and pinned helper versions in one place.
		- Fuzz the nvlist decoder and the label and uberblock parsers.
		- Lint output kept with rotation and a `--check` gate.
		- Sync from remote before a run.
		- Packaging and checksums once there's a release.
		- Sweeping override, 2026-10-24: this supersedes any earlier decision on this project that conflicts with it.

## Old format

### Bugs

### Features and enhancements

- Build, CI/CD, and install
	- 🔘 A CI/CD pipeline kicked off by a bash script (`cicd/cicd.bash`): builds, tests, and can commit and push. Packaging and publishing are opt-in.
		- 2026-10-24: superseded by 2026102416291700 and the other `CICD reset` items.
	- 🔘 Dev-environment install script (Linux bash, macOS sh, Windows PowerShell), runnable via a single `curl`/`wget`. Clones main, installs dependencies, and states what it will do with an option to abort.
	- 🔘 Release-install script per platform, runnable via a single `curl`/`wget`. Downloads, installs, and runs the latest release, with an option to abort.

- Configuration and persistence

	- 🔘 Default configuration hard-coded
		- 🔘 Overridden by per-user config file, created the first time a default setting is changed.
			- 🔘 Settings live under `~/.config` (YAML or TOML), resistant to errors (e.g. don't bail on the whole thing due to one bad line).
		- 🔘 Overridden by program options at run-time.

- Phase 0 - foundation

	- 🛠️ Repo, license, provenance, clean-room process, workspace skeleton
		- ✅ GPL-2.0-or-later license, notice, provenance, contributing
		- ✅ clean-room process document
		- ✅ Rust workspace (`zfsgpl-ondisk`, `zfsgpl-core`, `zfsgpl-cli`)
		- ✅ Design and backlog docs
		- ✅ Set up the spec repo (`zfs-gpl-spec`) and wire the dirty tree with its own role-constraining context (`DIRTY-SIDE.md`, openzfs pinned)
		- 🔘 CI: build, test, fmt, clippy (the clone-detection tripwire runs spec-side, not here - see Phase 1)
			- 2026-10-24: superseded by 2026102416291700 and the other `CICD reset` items.
		- 🔘 rustfmt/clippy pre-commit hook

- Phase 1 - legal groundwork (parallel, some for counsel)
	- 🛠️ Physical wall: isolated spec environment on a separate system (no network/filesystem path to this one), with its own agent installation, instructions, memory, and settings
		- Dirty tree and spec working tree move there; no OpenZFS source copy remains on the implementation system
	- 🔘 Similarity audit script (spec-side): lexical harvest (identifiers/strings/comments/constants) of this repo vs pinned source, allowlist from approved specs, results to the gatekeeper log
	- 🛠️ Freedom-to-operate patent search on Sun/Oracle ZFS patents and third-party filesystem patents (counsel-led); `legal/patent-fto.md`. Preliminary bibliographic inventory done 2026-07-20 (live vs expired, real dates) but kept in PRIVATE notes, not public (willfulness caution); counsel-led claim reads + two gaps (RAID-Z parity, foundational COW grant) still open
	- 🔘 Counsel review of cleanroom.md (incl. the shared-model section) and the CDDL-patent-grant trade-off
	- 🔘 Confirm the published 2006 spec is the format-of-record for the pre-2006 core, and catalogue what it does and does not cover

- Phase 2 - read the core format
	- 🛠️ Uberblock: parse + endianness + active-uberblock ranking done (`uberblock.rs`); device I/O layer now scans real slots
		- ✅ Device I/O seam: `BlockDevice` trait + `FileDevice` (image or raw device), portable positioned reads (`device.rs`)
		- ✅ Leaf-vdev scan: read all readable labels, discover uberblock candidates at 1 KiB stride (ashift-independent), rank to the active one (`vdev.rs`); wired to `zgpl scan <path>`
		- ✅ Self-checksum gate (spec 8.1 step 3): each candidate must self-checksum against its device offset; tries all slot sizes so it stays ashift-independent
	- 🔘 Block pointers and DVAs: decode, follow, verify checksums (fletcher4, SHA-256)
	- 🔘 DMU: dnodes and object sets
	- 🔘 ZAP: micro and fat
	- 🔘 DSL: enumerate datasets and snapshots
	- 🔘 ZPL: read files and directories
	- 🔘 `zgpl` read-only: import a pool and list/read a dataset

- Phase 3 - modern format features (via clean-room spec pipeline)
	- 🔘 Feature flags: detect and gate
	- 🔘 Compression: lz4, zstd, gzip
	- 🔘 Checksums beyond the core: edonr, blake3, skein
	- 🔘 Native encryption (note: illumos vs OpenZFS formats differ)
	- 🔘 dRAID and raidz geometry
	- 🔘 Log spacemaps, large dnodes, large/embedded blocks

- Phase 4 - write path (greenfield)
	- 🔘 Allocation and spacemaps
	- 🔘 Transaction groups and the copy-on-write commit
	- 🔘 ZIL
	- 🔘 Create/modify/snapshot, round-trip verified against OpenZFS as external oracle

- Phase 5 - system integration
	- 🔘 Native OS caching design and implementation
	- 🔘 Native device discovery (no cache-file dependence)
	- 🔘 Delivery form: kernel module vs FUSE vs userspace, decided and built
	- 🔘 Coexistence validation with a live OpenZFS install

- Testing (ongoing)
	- 🔘 Independent conformance vectors from the spec
	- 🔘 Black-box interop harness: round-trip pools between zfs-gpl and stock OpenZFS
	- 🔘 Derived (not copied) test cases expanding coverage over time

### Done

#### Done - Bugs

#### Done - Features and enhancements

- Phase 1 - legal groundwork (parallel, some for counsel)
	- ✅ Clean-room process v2: physical wall, single crossing point + request channel, similarity audit, evidence retention, shared-model section (`cleanroom.md`)
	- ✅ Request channel: `requests.md` in the spec repo - questions in, approved specs out, all logged in git
	- ✅ Evidence retention: transcript retention raised, daily append-only archive with SHA-256 manifest under `private/` (outside this repo)
	- ✅ Stand up the spec pipeline: dirty-side analysis -> gatekeeper review -> spec repo, with the evidence trail (first spec: label+uberblock, `7f86d1b`)

- Phase 2 - read the core format
	- ✅ Vdev labels: geometry/region math (`label.rs`), self-checksum validation (`checksum.rs`), XDR nvlist parse (`nvlist.rs`, spec 03 - all 26 types, nested lists, encoded-size resync). Remaining: read the config off a device (verify region-3 checksum, decode, extract identity) - tracked under read-only import below
	- ✅ Label/uberblock self-checksum: offset-anchored SHA-256 (spec 6), digest-to-word packing per spec 02. Own SHA-256 (`sha256.rs`, FIPS 180-4), no crypto dep; verified against FIPS + spec-02 packing vectors

### Deferred

### Canceled

## Template

### Old format

- 🔘 Not started

- 🛠️ Started, and/or partially complete

- 🔬 Testing not started or finished

- ✋ Defer

- ✅ Complete

- 🚫 Canceled

### New format

- Notes:

	- Only use rows that you actually need or expect will be filled in. Always fill in the title, ID, Type, Status, Opened and Created by.

	- The ID is the local time to the hundredth of a second. Opened is when it was written down, which may differ. (Use a keyboard macro and possibly something like project 'zuid' to generate.)

	- Status values meaning: Testing means the fix is in and checks are running or still to run. Waiting on signoff means automated testing passed. Moot means something else changed that made it irrelevant. Canceled means it still applies but was decided against. Waiting for testing means the fix is in and waits on a long CI run or an outside test host. Can't reproduce means a real attempt to reproduce it failed.

	- As issues are worked, and statuses change, place them in correct sorting order within the list:
		- First by status: Waiting for answers, Waiting on signoff, Testing, Waiting for testing, Can't reproduce, Stalled, Started, Queued, Done, Deferred, Canceled, Moot
		- Then by severity|priority: Critical, High, Avg, Low
		- Then by type: Bugs, [not bugs together]

	- Rows marked [Bug] are for bugs only, and rows marked [Feature] for features and enhancements. Children are not nested. They sit at the top level and point back with Parent ID.

Template:

- Title
	- ID: YYYYmmDDHHMMSSNN
	- Type: [Bug|Feature|Enhancement|Task]
	- Status: [Queued|Waiting for answers|Waiting on signoff|Waiting for testing|Started|Testing|Stalled|Can't reproduce|Moot|Canceled|Deferred|Done]
	- Needs local test suite run?:
	- Needs external testing:
	- Priority|Severity [Bug]: [Critical|High|Avg|Low]
	- Opened:
	- Opened by:
	- Assigned to:
	- Parent ID:
	- Prereq IDs:
	- Related IDs:
	- Target OS:
	- Test environment:
	- Version and build:
	- Requirements  [Feature]:
		- Hierarchical bulleted list.
	- Steps to reproduce [Bug]:
		- …
	- Incorrect behavior [Bug]:
	- Expected behavior [Bug]:
	- Reproduced [Bug]: [No, or when, where and how]
	- Possible cause [Bug]:
	- Actual cause [Bug]:
		- …
	- Estimated effort: [High|Avg|Low]
	- Actual effort: [High|Avg|Low]
	- Progress log:
		- …
	- Decisions:
		- …
	- Actual fix [Bug]:
	- Branch:
	- Commit:
	- Test case: [Reason not applicable, or CI test case #]
	- Acceptance signoff:
	- Superseded by ID:
	- Closed:
