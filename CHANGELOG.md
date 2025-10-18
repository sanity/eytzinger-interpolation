# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.1] - 2025-10-18

### Fixed

- **Critical**: Fixed benchmark crate references from `eytzinger::` to `eytzinger_interpolation::`
- **Critical**: Fixed documentation examples to use correct crate name `eytzinger_interpolation::`
- Fixed documentation typo in interpolative search description

### Added

- Comprehensive edge case tests for interpolative search:
  - Empty array test
  - Single element test
  - All equal elements test
  - Below minimum value test
  - Above maximum value test
  - Between values test
- Property-based test for interpolative search bounds correctness

### Changed

- Updated repository URL to `https://github.com/sanity/eytzinger-interpolation`

## [1.0.0] - 2025-10-18

### Added

- Initial release of `eytzinger-interpolation` fork
- `eytzinger_interpolative_search_by` method for finding bounds around a search value
- `eytzinger_interpolative_search` method (convenience wrapper)
- `eytzinger_interpolative_search_by_key` method for key-based searches
- All features from upstream `eytzinger` v1.1.1
- Comprehensive README documentation
- GitHub Actions CI/CD workflows
- MIT license (matching upstream)

### Changed

- Package name from `eytzinger` to `eytzinger-interpolation`
- Updated documentation to reference new package name

### Credits

- Fork of [rust-eytzinger](https://github.com/main--/rust-eytzinger) by [main()](https://github.com/main--)
- Interpolative search additions by [Andre Popovitch](https://github.com/anchpop)
- Published and maintained by [Ian Clarke](https://github.com/sanity)

## [Unreleased]

No unreleased changes yet.

---

[1.0.0]: https://github.com/sanity/eytzinger-interpolation/releases/tag/v1.0.0
