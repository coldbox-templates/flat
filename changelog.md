# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

* * *

## [Unreleased]

## [8.0.0s] - 2025-10-10

## [7.4.0] - 2025-06-07

### Added

- More maven pom.xml files for better IDE support

### Fixed

- Gitignore updates so it doesn't ignore 'config/modules'

## [7.3.0] - 2023-05-19

### Fixed

- Changed `renderView()` to new standard of `view()`
- Added `allowPublicKeyRetrieval=true` to the `db` connection string
- Added missing bundle name and version in `.cfconfig.json` and `.env.example`

## [7.2.0] - 2023-05-16

### Fixed

- Added correct dependency versions

## [6.20.0] => 2023-MAR-20

### Added

- Added routing conventions to make it easier for the cli to add routes.

## [6.19.0] => 2023-MAR-20

### Added

- Forgot the `modules_app` convention.

## [6.18.0] => 2023-MAR-18

### Fixed

- GH actions

## [6.17.0] => 2023-MAR-18

### Added

- Changelog Tracking
- Github actions for auto building
- Latest ColdBox standards
- UI Updates
- Latest Alpine + Bootstrap Combo
- vscode introspection and helpers
- Docker build and compose consolidation to the `build` folder
- Cleanup of `tests` to new standards

[unreleased]: https://github.com/coldbox-templates/flat/compare/v8.0.0s...HEAD
[8.0.0s]: https://github.com/coldbox-templates/flat/compare/v7.4.0...v8.0.0s
[7.4.0]: https://github.com/coldbox-templates/default/compare/v7.3.0...v7.4.0
[7.3.0]: https://github.com/coldbox-templates/default/compare/v7.2.0...v7.3.0
[7.2.0]: https://github.com/coldbox-templates/default/compare/4ff554bcb4383a973dbec39af57ce96667764cee...v7.2.0
