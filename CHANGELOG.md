# Changelog

All notable changes to the Karma Test Explorer extension will be documented in this file.

The format of this changelog is loosely based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), and this extension uses versioning similar to [semantic versioning](https://semver.org/spec/v2.0.0.html).

<details>
  <summary>Releases</summary>

  - [0.3.0 - Nov 6, 2021](#030---nov-6-2021)
  - [0.2.1 - Oct 24, 2021](#021---oct-24-2021)
  - [0.2.0 - Oct 13, 2021](#020---oct-13-2021)
  - [0.1.0 - Sep 28, 2021](#010---sep-28-2021)
</details>


---
## [0.3.0] - Nov 6, 2021

### Added

- New `karmaTestExplorer.nonHeadlessModeEnabled` extension setting for running tests in non-Headless mode
- New `karmaTestExplorer.karmaReporterLogLevel` extension setting for specifying the level of logging detail for Karma Test Explorer's Karma reporter plugin

### Changed

- Karma Test Explorer is now only activated for a workspace folder if it contains one or more Karma Test Explorer configuration settings, or a known standard config file for Karma or Angular projects exists somewhere under the project folder tree, with the exclusion of the `node_modules` folder

### Fixed

- Fixed an [issue](https://github.com/lucono/karma-test-explorer/issues/9) where the extension fails to start for Windows users if the user's profile path contains a space
- Fixed an [issue](https://github.com/lucono/karma-test-explorer/issues/10) where test discovery or execution sometimes fails on a Karma error indicating that some of the tests performed a full page reload
- Fixed an [issue](https://github.com/lucono/karma-test-explorer/issues/7) where some Karma reporters configured in the user's Karma config file would cause the extension to fail to start
- Fixed an issue which increases the number of test failure scenarios where the precise test expectation that failed can be highlighted. Previously, only the parent test containing the failed expectation was ever highlighted
- Fixed an issue where changes to test files, and changes to the Karma config and other watched files, were not always detected and reflected in the test view and did not always trigger the appropriate refresh behavior

---
## [0.2.1] - Oct 24, 2021

### Changed

- Test duplication is no longer reported for test suites because test suites are simply containers for tests, so that duplicated test suites are themselves not an indication of actual test duplication

### Fixed

- Fixed an issue where test duplicate detection was producing false-positives on Windows (thanks [@nwash57](https://github.com/nwash57)!)
- Fixed an issue where some tests may not always be discovered on Windows

---
## [0.2.0] - Oct 13, 2021

### Added

- Automatic detection of the test framework in use by the project
- Automatic detection of when testing in a container to apply helpful optimizations
- New prompt for applying settings updates when they are changed
- New `karmaTestExplorer.angularProcessCommand` config setting for specifying a custom command or executable for Angular
- New `karmaTestExplorer.failOnStandardError` config setting that can be useful for uncovering testing issues

### Changed

- Watch mode (the `autoWatchEnabled` setting) is now enabled by default
- When not set, the `autoWatchBatchDelay` setting now defaults to the configured or default value in the project's Karma config file. Previously, this value always defaulted to 5 secs and you had to explicitly set it to the same value as the project Karma config if desired
- The `karmaTestExplorer.karmaProcessExecutable` config setting has been renamed to `karmaTestExplorer.karmaProcessCommand`, aligning the naming of both it and the newly added `karmaTestExplorer.angularProcessCommand` setting
- The `karmaTestExplorer.containerModeEnabled` boolean setting has been renamed to an enum `karmaTestExplorer.containerMode` setting, with possible values of `auto` (the default when not set), `enabled`, or `disabled`. Without updating existing pfoject configurations, this should not casue any change in behavior for projects already using the old setting to enable container mode because the new setting's default value of `auto` will allow container-based environments to still be detected and optimized by default
- Test files that are auto-detected by default has expanded to also include filenames starting with `test` or `spec` or `unit`, followed by a dot (`.`) or a hyphen (`-`) or an underscore (`_`). Previously, only those ending with `test` or `spec` or `unit`, preceded with a dot (`.`) or a hyphen (`-`) or an underscore (`_`) would be detected by default
- The `node_modules` folder is now always excluded from search during test discovery even if the `karmaTestExplorer.excludeFiles` setting is specified without explicitly having `node_modules` on the excluded list. Previously, this would cause `node_modules` not to be excluded

### Fixed

- Fixed [an issue](https://github.com/lucono/karma-test-explorer/issues/2) (#2) where spaces in the user's home directory or the extension installation path caused the extension to fail for Windows users
- Fixed issue where line numbers shown in warning messages for detected duplicate test definitions were off by one line

---
## [0.1.0] - Sep 28, 2021

### Added

- Mocha test framework support
- Karma version 6 support
- Support for [Dev Containers](https://code.visualstudio.com/docs/remote/containers)
- Watch mode support for the Jasmine test framework with continous pass / fail status update
- Support for grouping tests by folder in addition to existing support for grouping by test suite
- Passed, failed, skipped, total count, and execution time stats for tests in the Test view side bar
- Detection and flagging of duplicate tests in the Test view side bar
- Environment variable support directly in the extension settings or via a `.env` file
- Support for using custom launchers defined in the Karma config or defining one directly in extension settings
- Support for using a custom Karma executable or script
- Support for automatically reloading Karma on changes to the Karma config file
- Support for using a different Karma port than the one in the Karma config for testing in VS Code
- Dedicated `Karma Server` output channel for viewing the Karma server log in VS Code

### Changed

- By default, tests are now grouped by folder rather than by test suite
- Various additional test file naming schemes other than `*.spec.ts` are also now detected by default
- Significantly improved logging and error handling
- More resilient port management to prevent port conflicts

### Fixed

- Fixed various scenarios where code lens would not be rendered due to file and line location of tests not being detected

---
## See Also

- [Readme](https://github.com/lucono/karma-test-explorer/blob/master/README.md#karma-test-explorer-for-visual-studio-code)
- [Documentation](https://github.com/lucono/karma-test-explorer/blob/master/docs/documentation.md#documentation---karma-test-explorer)
- [Contributing](https://github.com/lucono/karma-test-explorer/blob/master/CONTRIBUTING.md#contributing---karma-test-explorer)