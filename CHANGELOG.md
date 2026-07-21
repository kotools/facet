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

- The `@Faceted` annotation to the `facet-core-dsl` module, marking a class as a
  _faceted class_ with multiple compile-time projections ("facets"), and its
  associated compile-time checks to the `facet-core-ksp` module.
- The `@ExperimentalKotoolsFacetApi` annotation to `facet-core-dsl`, indicating
  that a declaration is experimental and can be incompatibly changed in the
  future. See also our [versioning strategy] and [declarations lifecycle].
- The `@KotoolsFacetDsl` annotation to `facet-core-dsl`, indicating that a class
  declaration is part of Kotools Facet's DSL.
- The `FacetHost` interface to `facet-core-dsl`, providing access to facet
  definitions, and its associated compile-time checks to `facet-core-ksp`.

<!----------------------------------- Links ----------------------------------->

[declarations lifecycle]: documentation/declarations-lifecycle.md
[Keep a Changelog]: https://keepachangelog.com/en/2.0.0
[versioning strategy]: documentation/versioning-strategy.md
