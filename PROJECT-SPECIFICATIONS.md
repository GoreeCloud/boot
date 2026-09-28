# GoreeCloud Boot — Project Specifications

**Document Type:** Repository-Native Project Specification  
**Status:** Active specification / Development  
**Project:** GoreeCloud Boot  
**Repository:** GoreeCloud/boot  
**Authority:** Repository-local project specification  
**License:** GPL-3.0-or-later for GoreeCloud-owned source  
**Last Updated:** 2026-09-27

## 1. Product Definition

GoreeCloud Boot is GoreeCloud's native, open-source multiboot removable-media platform for booting, installing, recovering, diagnosing, and maintaining operating systems and GoreeCloud environments.

Core boot and provisioning functions must remain useful offline and must not require a GoreeCloud account, subscription, vendor cloud, hosted control plane, advertising, behavioral analytics, or mandatory telemetry.

Ventoy is a capability reference only. GoreeCloud Boot is not a Ventoy fork and must not depend on Ventoy source code for its product identity or architecture.

## 2. Current Lifecycle and Implementation Boundary

GoreeCloud Boot is in Development.

The authoritative default branch currently contains repository documentation but no accepted product implementation. Draft pull request #1 contains the current native Rust development foundation. Its exact head as of 2026-09-27 is 5a6cfd0121068aa80cafc51c2c5d33dedf8e83a2, and CI run 34160325218 completed successfully.

That draft candidate includes read-only Linux device discovery, bounded storage-topology and visible mount-namespace analysis, active-swap exclusion, conservative target assessment, sector-aware GCBOOT/GCDATA planning, GPT metadata generation, catalog validation, and development-only regular-file GPT image tooling.

The candidate does not establish physical block-device write authority, filesystem creation, a bootable USB release, a UEFI runtime, Secure Boot, compatibility certification, production approval, RC status, or Stable status.

## 3. Native Development Boundary

GoreeCloud Boot must be developed from GoreeCloud requirements rather than by importing another multiboot product as the implementation baseline.

Mature open-source boot technologies may be used as bounded foundations when licensing, provenance, security, architecture, and maintenance requirements are satisfied. GoreeCloud owns the product-specific provisioning logic, catalog model, safety controls, update model, verification policy, configuration model, user experience, tests, and release process.

Third-party source must not be copied into GoreeCloud-owned modules without a compatible license, a documented engineering purpose, and preserved provenance.

## 4. Supported Environment and Initial Targets

The initial administration environment is Linux, including representative Zorin OS workstations.

The initial firmware target is UEFI x86-64.

Future support for ARM64, Secure Boot, legacy BIOS, iPXE-based network boot, persistence, Windows installation media, WIM flows, raw-disk images, and virtual-disk formats must be treated as separately implemented and validated capabilities rather than assumed compatibility.

## 5. Core Architecture

### 5.1 Boot Core

The boot core must discover the GoreeCloud Boot device, load trusted configuration, enumerate supported boot entries, enforce applicable integrity policy, and dispatch through explicitly supported boot methods.

Boot-system updates should be separable from user image/data storage so routine runtime maintenance does not require recreating the entire device.

### 5.2 Image Catalog

The image catalog must describe bootable assets without modifying their original content by default.

Catalog metadata may include display name, asset type, architecture, checksum, signature, persistence configuration, unattended-installation data, compatibility mode, and boot parameters.

Malformed or hostile metadata must fail safely.

### 5.3 Host Provisioning Utility

A native host utility, provisionally named bootctl, is responsible for supported device preparation, GoreeCloud Boot installation and updates, catalog verification, boot-partition repair, device inspection, and later governed provisioning workflows.

The initial supported administrative workflow should remain reliable from the command line before a graphical manager is treated as required.

### 5.4 Preboot Interface

The preboot interface must use Glaze UI principles only to the extent that the firmware environment can substantively support them.

Requirements include clear hierarchy, strong focus indication, keyboard navigation, readable typography, high-contrast states, restrained motion, explicit destructive-action language, and progressive disclosure.

Documentation must not claim full desktop Glaze UI parity where firmware limitations prevent it.

## 6. Storage Layout

The default removable-media layout is planned around GPT with a protective MBR where compatible.

### GCBOOT

GCBOOT is the boot-system partition. It is planned as a small FAT32 partition containing the UEFI boot chain, GoreeCloud Boot runtime, configuration, trusted verification material, and recovery metadata.

Routine image management should not require users to manipulate GCBOOT directly.

### GCDATA

GCDATA is the large user-facing data partition. exFAT is the planned default filesystem for cross-platform large-file support, subject to implementation and compatibility validation.

Supported ISO, IMG, EFI, WIM, VHD/VHDX, persistence data, checksums, signatures, and sidecar metadata may be stored on GCDATA according to supported boot methods.

Routine GoreeCloud Boot updates must preserve GCDATA by default.

Persistence should use files or explicitly managed partitions rather than silently repartitioning a device.

## 7. Boot Compatibility Model

GoreeCloud Boot must not claim universal arbitrary-image compatibility.

Each boot path and image family must have an explicit support level backed by relevant test evidence.

The first implementation should prioritize:

- direct UEFI application launch;
- selected Linux installation or live-image paths with documented loopback, kernel/initrd, or chainload behavior;
- catalog integrity verification;
- non-destructive boot-runtime maintenance;
- QEMU/OVMF validation before physical-device acceptance.

Windows installation media requires a dedicated compatibility implementation rather than being treated as equivalent to Linux ISO booting.

## 8. Device and Destructive-Operation Safety

Provisioning is a destructive-capability domain and must be designed around preventing wrong-disk writes.

Before physical writes can be enabled, the product must provide and validate all applicable controls, including:

- positive removable-target identification;
- stable/current-instance identity evidence;
- display of target identity and capacity;
- default rejection of obvious system disks;
- topology-aware rejection of active host storage relationships;
- mounted-filesystem and active-swap exclusion;
- sufficient mount-namespace visibility for the supported execution environment;
- explicit user authorization before destructive changes;
- fresh revalidation immediately before writes;
- fail-closed behavior when identity, geometry, topology, namespace, mount, swap, or other critical evidence changes or becomes incomplete;
- write-plan provenance;
- production-unique GPT identity generation;
- safe write ordering and interruption recovery;
- post-write verification;
- representative physical-media validation.

A successful assessment or revalidation token is evidence for planning only. It must never, by itself, become destructive-operation authorization.

The existing draft implementation deliberately keeps destructive_write_authorized false and contains no physical block-device write path.

## 9. GPT and Layout Requirements

Layout arithmetic must use checked operations and explicit logical-block geometry.

The design must support protective MBR data, primary and backup GPT headers, partition-entry arrays, required CRC32 fields, and validated usable ranges.

GCBOOT uses the EFI System Partition type. GCDATA uses a general data partition type appropriate to the supported filesystem and platform requirements.

Development tooling may create GPT metadata in new regular files for testing, but a regular-file test image must not be represented as a bootable product image unless boot/runtime/filesystem functionality has actually been added and validated.

## 10. Security Requirements

GoreeCloud Boot must apply applicable GoreeCloud security governance and maintain a fail-closed posture around trust-critical operations.

Requirements include:

- release provenance and exact-source traceability;
- checksum and detached-signature verification where applicable;
- explicit verified and unverified image states;
- tamper detection;
- safe update policy;
- malicious or malformed metadata handling;
- network-boot restrictions;
- least privilege;
- dependency and supply-chain review;
- secrets and signing-material protection;
- safe handling of destructive operations;
- recovery guidance when verification fails.

Trusted GoreeCloud release components should fail closed when their required integrity verification fails.

Unverified third-party images may be allowed only under an explicit user policy appropriate to the lifecycle stage and must not be visually represented as trusted.

## 11. Privacy Requirements

Core operation is local and offline-first.

The product must not include advertising, tracking, behavioral analytics, or mandatory telemetry.

Image names, checksums, device identifiers, boot history, and local configuration must not be transmitted merely to use the product.

Any optional network feature must disclose its destination and purpose and minimize transmitted information.

## 12. Recovery and Continuity Requirements

GoreeCloud Boot must be recoverable without dependence on a proprietary hosted service.

Recovery requirements include:

- preservation of boot-system configuration and image/persistence metadata;
- repair of damaged GCBOOT contents without unnecessary GCDATA destruction;
- exportable configuration;
- documented reconstruction procedures;
- recovery metadata;
- restoration testing;
- release artifacts and source sufficient to rebuild supported environments.

A device should be reconstructable from documented source, release artifacts, configuration, and user-owned image data.

## 13. GoreeCloud Platform Integrations

### Wardveil Security

Wardveil responsibilities include release provenance, runtime integrity policy, trust-state handling, malicious metadata defenses, boot-entry verification, and response guidance when integrity checks fail.

### Privacy Shield

Privacy Shield requirements reinforce local-first operation, data minimization, explicit network behavior, and the prohibition on unnecessary telemetry.

### Everkeep

Everkeep responsibilities include recoverability, preservation of configuration and metadata, reconstruction guidance, and restoration validation.

### GoreeCloud Mesh

Mesh may later provide optional coordination for host-side management, capability reporting, lifecycle events, device inventory, and GoreeCloud Manager visibility. Mesh must never become a boot-time dependency for ordinary local use.

### GoreeCloud Identity

Interactive Identity authentication is not required for the initial offline boot menu.

Identity becomes applicable to privileged host administration, delegated device management, centrally managed trust policy, or authenticated network services.

Boot trust must derive from cryptographic verification and policy, not a cosmetic login requirement.

## 14. Third-Party Foundations and Licensing

GNU GRUB is a candidate bounded bootloader foundation under GPLv3-or-later.

EDK II is a candidate UEFI development foundation whose main codebase is primarily BSD-2-Clause-Patent with additional component licenses.

iPXE may be used as an optional, separately built network-boot component subject to its file-level licensing.

GoreeCloud-owned Boot source is governed by GPL-3.0-or-later unless a later authoritative project-specific licensing decision supersedes it.

Distributed builds must preserve required notices, source availability obligations, component provenance, dependency inventory, and SBOM/provenance material when supported.

GPLv2-only material must not be combined into a GPLv3-only work without a verified compatible distribution model.

## 15. Build, Test, and Release Requirements

Automated validation should cover, as applicable:

- formatting and linting;
- unit tests;
- catalog and configuration validation;
- layout and GPT generation;
- filesystem and partition safety;
- malformed metadata;
- checksum and signature failures;
- storage-topology and active-use evidence;
- mount-namespace visibility behavior;
- interruption and recovery;
- artifact provenance;
- dependency and license checks.

Virtual boot validation should use QEMU and OVMF where suitable.

Physical validation must cover representative UEFI systems and removable-media devices before Stable status is considered.

Image compatibility must be tracked by image family and version rather than inferred from a single successful boot.

Release artifacts must be traceable to exact source revisions and include appropriate checksums, signatures when the signing system is established, dependency/license information, and upgrade/recovery instructions.

## 16. Initial Engineering Milestone

The first product milestone is a bootable UEFI x86-64 prototype that can:

1. provision a supported test USB device with GCBOOT and GCDATA;
2. present a GoreeCloud Boot menu;
3. discover explicitly supported entries;
4. directly launch supported EFI applications;
5. boot at least one validated Linux image path;
6. verify catalog checksums;
7. update GCBOOT without erasing GCDATA; and
8. complete QEMU/OVMF validation before physical-device acceptance.

This milestone is not, by itself, a Stable release.

Secure Boot, Windows-media compatibility, persistence, ARM64, network boot, and legacy BIOS remain outside the first milestone unless independently implemented and validated without weakening the safety boundary.

## 17. Roadmap

### Phase 0 — Foundation

Establish the project specification, repository baseline, dependency and license review, threat model, disk-format specification, configuration schema, and test matrix.

### Phase 1 — UEFI x86-64 Prototype

Implement UEFI x86-64 provisioning, GCBOOT/GCDATA, the boot catalog, direct EFI launch, selected Linux-image support, integrity verification, non-destructive boot updates, and virtual-machine tests.

### Phase 2 — Broader Compatibility and Recovery

Add dedicated Windows installation-media support, persistence workflows, stronger recovery tooling, compatibility reporting, and broader physical-hardware validation.

### Phase 3 — Advanced Platform Capabilities

Evaluate validated Secure Boot, ARM64, optional iPXE network boot, a graphical host manager, and deeper GoreeCloud Manager or Mesh integration.

Legacy BIOS support remains deferred until justified by verified GoreeCloud requirements and sustainable testing cost.

## 18. Acceptance and Stable-State Requirements

No capability may be described as implemented merely because it is specified or exists only in an unmerged branch.

No physical provisioning capability may be accepted until the destructive-operation safety model and representative hardware evidence satisfy the applicable release gates.

A Stable classification requires evidence appropriate to the claimed scope, including representative boot/runtime behavior, recovery, compatibility, safety, release provenance, and supported-hardware validation.

Source-level CI success alone does not establish production or Stable acceptance.

## 19. Maintenance and Retirement

This file must be updated whenever material scope, architecture, supported platforms, boot methods, storage layout, security requirements, privacy requirements, integrations, acceptance gates, or lifecycle decisions change.

Significant project history and evidence belong in PROJECT-RECORD.md.

Feature lifecycle state belongs in IMPLEMENTED-FEATURES.md and PLANNED-FEATURES.md.

Release-oriented change history belongs in CHANGELOGS.md.

The repository, not Google Drive, is the authoritative location for GoreeCloud Boot project specifications and project records after migration acceptance.
