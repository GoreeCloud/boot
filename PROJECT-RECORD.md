# GoreeCloud Boot — Project Record

**Document Type:** Repository-Native Project Record  
**Status:** Active  
**Project:** GoreeCloud Boot  
**Repository:** GoreeCloud/boot  
**Authority:** Repository-local project record  
**Last Updated:** 2026-09-27

## 2026-09-27 — Repository-local project specification migration staged

GoreeCloud Boot's project-governance record is being migrated from its prior GoreeCloud Drive specification into the repository-mandated PROJECT-SPECIFICATIONS.md and PROJECT-RECORD.md model.

The migration reconciles the historical repository name GoreeCloud/goreecloud-boot to the live repository GoreeCloud/boot and separates normative product requirements from implementation history.

The prior Drive specification remains a protected migration source until the migration is accepted on the authoritative default branch and read back successfully. Permanent Drive removal is required only after that gate is satisfied.

The active implementation candidate remains draft pull request #1. This documentation migration does not merge, promote, or otherwise treat that candidate as accepted implementation.

## 2026-09-27 — Repository-native feature-state records established on main

The accepted default branch contains repository-native PLANNED-FEATURES.md, IMPLEMENTED-FEATURES.md, and CHANGELOGS.md.

Those records retired Drive-side feature-roadmap synchronization and preserve a fail-closed boundary: planned work is not treated as implemented without authoritative evidence.

At this point, main still does not contain an accepted product implementation.

## 2026-09-27 — Live implementation candidate verified

Draft pull request #1, "Bootstrap native storage and mount-namespace safety foundation," remains open and unmerged.

Its exact head is:

5a6cfd0121068aa80cafc51c2c5d33dedf8e83a2

GitHub Actions CI run 34160325218 completed successfully on that exact head.

The candidate contains a native Rust Development foundation with:

- conservative target assessment;
- read-only Linux whole-device discovery;
- recursive bidirectional sysfs holders/slaves topology traversal;
- visible mount-namespace enumeration and unioned readable mount evidence;
- fail-conservative handling of incomplete visible namespace coverage;
- mounted-filesystem and active-swap rejection;
- topology-, namespace-, active-use-, identity-, and geometry-aware revalidation evidence;
- deterministic GCBOOT/GCDATA planning;
- GPT metadata generation and CRC validation;
- catalog validation; and
- development-only regular-file GPT image creation with read-back verification.

The candidate deliberately contains no physical block-device write path.

Its TargetAssessment destructive_write_authorized behavior remains false, so an eligible assessment or matching revalidation token cannot be treated as authorization to write a physical device.

The candidate does not establish filesystem creation, UEFI runtime, bootable release artifacts, Secure Boot, Windows-media support, persistence, ARM64, network boot, physical-device acceptance, production readiness, RC, or Stable status.

## 2026-09-07 — Non-destructive Linux provisioning plan checkpoint

Development head 5a6cfd0121068aa80cafc51c2c5d33dedf8e83a2 introduced a non-destructive LinuxProvisioningPlan that binds planned sector layout to the discovered target devnode, exact LinuxRevalidationToken, current target eligibility, and device geometry.

Fresh read-only revalidation reports whether path identity, replacement/topology evidence, safety eligibility, and layout geometry still match the plan.

Replacement, newly active use, mounted state, or other relevant safety changes invalidate the planning evidence.

Even an exact fresh match does not authorize destructive writes.

Separate destructive authorization, immediate pre-write target revalidation, hardware acceptance, rollback/recovery validation, and production qualification remain outstanding.

## 2026-09-07 — Absolute and normalized target-path guards

Development checkpoints added conservative path requirements to generic target assessment.

A target path must be non-empty, absolute, and lexically normalized; relative paths and paths containing dot or dot-dot traversal components are rejected.

An attempted generic requirement to force /dev paths was not accepted because the same assessment primitive is deliberately exercised against synthetic read-only fixture roots. Real device-node identity remains the responsibility of Linux discovery and revalidation.

These guards are planning safeguards only and do not authorize physical writes.

## 2026-09-06 — Absolute target-path planning safeguard

The Development target-assessment primitive was strengthened to reject relative device paths.

Regression coverage verified that relative target text cannot become an eligible target and still cannot authorize a destructive write.

Physical provisioning, filesystems, boot runtime, QEMU/OVMF acceptance, physical-device acceptance, Secure Boot, recovery qualification, RC, Stable, and production readiness remained outstanding.

## Product direction preserved from the pre-migration specification

GoreeCloud Boot is an original GoreeCloud-native multiboot and recovery platform rather than a Ventoy-derived product.

The project is intended to support offline-first local use, explicit image compatibility rather than universal compatibility claims, a GCBOOT/GCDATA storage model, strong wrong-disk protection, recovery-first maintenance, and bounded integration with GoreeCloud security, privacy, continuity, coordination, and identity systems.

GRUB, EDK II, iPXE, and other mature technologies may be used only as bounded third-party foundations subject to provenance, license, security, and architecture review.

## Repository-authority transition

Historical documentation identified Google Drive and the historical GoreeCloud/goreecloud-boot repository name as project authorities.

The current repository is GoreeCloud/boot.

After the project-specification migration is accepted and verified on the default branch, PROJECT-SPECIFICATIONS.md and PROJECT-RECORD.md are the authoritative project-governance records.

Feature state remains authoritative in IMPLEMENTED-FEATURES.md and PLANNED-FEATURES.md, and release-oriented history remains in CHANGELOGS.md.

## Open reconciliation item — draft PR #1 competing specification file

Draft PR #1 predates the repository-local project-record migration and currently contains a root SPECIFICATIONS.md file.

That file must not become a competing canonical specification.

Before PR #1 can be accepted, it must be reconciled against PROJECT-SPECIFICATIONS.md and either removed or converted into clearly supplementary, non-authoritative documentation. Any references in that branch to the historical GoreeCloud/goreecloud-boot repository name or Drive as current project authority must also be corrected.

Until that reconciliation and the migration PR's default-branch readback are complete, the Drive project-specification sources remain protected from deletion.
