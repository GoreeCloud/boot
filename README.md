# GoreeCloud Boot

GoreeCloud Boot is GoreeCloud's native, open-source multiboot removable-media platform for booting, installing, recovering, diagnosing, and maintaining operating systems and GoreeCloud environments.

**Lifecycle:** Development  
**Repository:** GoreeCloud/boot  
**License:** GPL-3.0-or-later for GoreeCloud-owned source

## Project authority

- [PROJECT-SPECIFICATIONS.md](./PROJECT-SPECIFICATIONS.md) — what GoreeCloud Boot is, must do, and must satisfy.
- [PROJECT-RECORD.md](./PROJECT-RECORD.md) — significant project history, decisions, migration evidence, and verified lifecycle events.
- [IMPLEMENTED-FEATURES.md](./IMPLEMENTED-FEATURES.md) — accepted implemented-feature state on the authoritative branch.
- [PLANNED-FEATURES.md](./PLANNED-FEATURES.md) — planned feature and obligation state.
- [CHANGELOGS.md](./CHANGELOGS.md) — release- and repository-oriented change history.

The GitHub repository is the authoritative location for project specifications and project records after the migration is accepted and verified.

## Current implementation boundary

The authoritative default branch does not yet contain an accepted GoreeCloud Boot product implementation.

Draft pull request #1 contains the current native Rust Development foundation for read-only Linux device discovery, conservative target assessment, storage-topology and visible mount-namespace evidence, active-swap rejection, GCBOOT/GCDATA planning, GPT metadata generation, catalog validation, and regular-file GPT test tooling.

That draft contains no physical block-device write path and does not establish a bootable release, filesystem creation, UEFI runtime, Secure Boot, compatibility certification, production readiness, RC, or Stable status.
