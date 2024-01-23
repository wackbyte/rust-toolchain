# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog],
and this project adheres to [Semantic Versioning].

## [Unreleased]

### Added

- `profile` determines which group of components is installed for the toolchain (defaults to `minimal`).
- `default` sets the installed toolchain as default (defaults to `false`).
- `override` sets the installed toolchain as the override for the current directory (defaults to `false`).
- More detailed documentation.

### Changed

- The installed toolchain is no longer set as default automatically. This is now controlled by `default`.

### Removed

- Rev-based toolchain version selection. This is now entirely controlled by `toolchain`.
- `target` in favor of `targets`, which it was an alias of.

[Unreleased]: https://codeberg.org/wackbyte/rust-toolchain/commits/branch/trunk

[Keep a Changelog]: https://keepachangelog.com/en/1.1.0/
[Semantic Versioning]: https://semver.org/spec/v2.0.0.html
