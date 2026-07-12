# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.2.0] - 2026-07-12

### Removed

- **darwin/amd64 (Intel) pre-built binary.** macOS releases now ship
  **arm64 only**, per the org-wide policy (darwin is Apple-Silicon only; no
  universal binaries). Intel Mac users can build from source.

### Changed

- **Linux release archives are now `.tar.gz`** (darwin/windows remain `.zip`),
  per `nlink-jp/.github` CONVENTIONS.md §Release Archive Standard. Archives
  still bundle `LICENSE` + `README.md` alongside the canonical binary.
- **darwin code-signature identifier** is now the canonical `sdate`
  (was `sdate-darwin-arm64`), set via `codesign -i` so it stays stable after
  the archived binary is renamed to its canonical name.

No change to the binary's behaviour — a packaging / build-config release.

## [1.1.3] - 2026-05-22

### Changed

- **Darwin releases are now Developer ID signed and Apple-notarized.**
  `sdate-v1.1.3-darwin-{amd64,arm64}.zip` carry full Apple Developer
  ID Application signatures and notarization tickets from Apple. End
  users on macOS no longer need to bypass Gatekeeper with right-click
  → Open or `xattr -d com.apple.quarantine` on first launch; local
  users who place `sdate` under Dropbox-synced (or any other
  FileProvider-managed) paths are no longer killed by macOS's
  ad-hoc + provenance distrust policy. Pipeline:
  `scripts/codesign-darwin.sh` + `scripts/notarize-darwin.sh`,
  driven by `make package`. Adopts the org-wide convention in
  `nlink-jp/.github` CONVENTIONS.md §Code Signing.

No behaviour change to the binary itself — feature-wise this is
identical to v1.1.2.

## [1.1.2] - 2026-03-28

### Changed
- Unified Makefile: replaced macOS universal binary with separate `darwin/amd64` and `darwin/arm64` targets; standardized targets (`build`, `build-all`, `test`, `lint`, `check`, `package`, `clean`, `help`) and output layout (`dist/` flat directory, `.zip` archives).

## [1.1.1] - 2026-03-28

### Internal

- Updated Go module path to `github.com/nlink-jp/sdate` following repository transfer to nlink-jp organization.

## [1.1.0] - 2025-08-28

### Added
- Change the start of the week to Sunday for `@w` snap operation.

### Fixed
- Fix a bug in parsing input strings where invalid inputs were not correctly identified.

## [1.0.0] - 2025-08-28

### Added
- Initial release of `sdate`.
- Command-line tool for Splunk-like time manipulation.
- Support for relative time and snap operations.
- Flexible output formatting, including UNIX timestamp.
- Timezone handling for base time and output.
- Unit tests for core logic.

### Changed
- Improved `Makefile` to provide comprehensive build, test, and packaging targets.
- `make package` now builds and archives for Linux, Windows, and macOS (Universal Binary).