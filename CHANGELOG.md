# 🔄 Changelog

All notable changes to this project will be documented in this file.

> The format of this document is based on [Keep a Changelog].

## 🤔 Types of changes

- `✨ Added` for new features.
- `♻️ Changed` for changes in existing functionality.
- `🗑️ Deprecated` for soon-to-be removed features.
- `🔥 Removed` for now removed features.
- `🐛 Fixed` for any bug fixes.
- `🔒 Security` for vulnerabilities.

## 🚧 Unreleased

### ✨ Added

- The `@Faceted` annotation, marking a class as a _faceted class_ with multiple
  compile-time projections ("facets"), validated at compile time via a KSP
  processor: a faceted class must be top-level, public or internal, a data
  class, and have a primary constructor that is public or internal; it should
  also declare a companion object.
- The `@ExperimentalKotoolsFacetApi` annotation, indicating that a declaration
  is experimental and can be incompatibly changed in the future. See also our
  [versioning strategy] and [declarations lifecycle] for more details.

<!----------------------------------- Links ----------------------------------->

[declarations lifecycle]: documentation/declarations-lifecycle.md
[Keep a Changelog]: https://keepachangelog.com/en/2.0.0
[versioning strategy]: documentation/versioning-strategy.md
