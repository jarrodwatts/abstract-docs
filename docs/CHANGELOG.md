```markdown
# CHANGELOG

## [1.4.5] - YYYY-MM-DD
### Added
- Added a new utility function `validateAddress` to ensure Ethereum addresses are valid, including checks for hex character validity.
- Introduced a `timeoutMs` parameter to the `isAGWAccount` function to handle potential timeouts during contract read operations.

### Changed
- Updated the `getAgwTypedSignature` function to include a `domainVersion` parameter, allowing for custom EIP-712 domain versioning. The default version is now "2.0.0".
- Added validation for the `messageHash` format in `getAgwTypedSignature` to ensure it is a 32-byte hex string.

### Fixed
- Improved error handling in `isAGWAccount` by implementing a timeout mechanism.

## [1.4.4] - YYYY-MM-DD
### Changed
- Updated package version to 1.4.4 in `package.json`.

## [1.4.3] - YYYY-MM-DD
### Changed
- Updated package version to 1.4.3 in `package.json`.

(Note: Replace `YYYY-MM-DD` with the actual release dates.)
```