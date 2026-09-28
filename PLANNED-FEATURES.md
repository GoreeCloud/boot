# GoreeCloud Boot — Planned Features

**Status:** Active repository-native roadmap control  
**As of:** 2026-09-27  
**Authoritative specification:** PROJECT-SPECIFICATIONS.md  
**Canonical repository:** GoreeCloud/boot

## Purpose

This file records planned GoreeCloud Boot feature and lifecycle work. It supplements PROJECT-SPECIFICATIONS.md and must not be used to turn plans into implementation claims.

Implementation status belongs in IMPLEMENTED-FEATURES.md. Significant project history belongs in PROJECT-RECORD.md. Release-oriented history belongs in CHANGELOGS.md.

## Roadmap

| ID | Feature / obligation | Priority | Current state |
| --- | --- | --- | --- |
| FR-001 | Maintain complete repository-local project specifications and project history, with no Drive copy retained after verified migration. | High | Migration candidate |
| FR-002 | Preserve the fail-closed physical-write boundary until destructive authorization, fresh revalidation, topology/active-use evidence, recovery behavior, and physical-device testing are accepted. | Critical | Required |
| FR-003 | Complete UEFI x86-64 provisioning with GCBOOT and GCDATA. | High | Planned |
| FR-004 | Implement the boot catalog, direct EFI launch, selected Linux image support, and integrity verification. | High | Planned |
| FR-005 | Validate QEMU/OVMF boot behavior before physical-device acceptance. | High | Planned |
| FR-006 | Add dedicated Windows installation-media support after the initial Linux/UEFI path is validated. | Medium | Planned |
| FR-007 | Add persistence workflows, stronger recovery tooling, compatibility reporting, and broader physical-hardware validation. | Medium | Planned |
| FR-008 | Evaluate Secure Boot, ARM64, optional iPXE network boot, graphical host management, and deeper Manager/Mesh integration only after their prerequisites are satisfied. | Medium | Future evaluation |
| FR-009 | Keep legacy BIOS deferred until verified GoreeCloud demand justifies its maintenance and test burden. | Low | Deferred |
| FR-010 | Reconcile draft PR #1 so its older SPECIFICATIONS.md cannot become a competing canonical project specification. | High | Required before PR #1 acceptance |

## Repository-native maintenance

Google Drive roadmap synchronization is retired.

At each material feature change, reconcile this roadmap against PROJECT-SPECIFICATIONS.md, verified repository implementation, applicable platform-system requirements, and GoreeCloud Tasks Management.

Missing obligations, stale status, duplicated work, roadmap drift, or undocumented disposition changes are defects to correct.
