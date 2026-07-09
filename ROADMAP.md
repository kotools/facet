# 🗺️ Roadmap

This roadmap outlines what's planned for Kotools Facet, starting with the first
stable release. It reflects current thinking and priorities, not a committed
timeline — plans may shift as the SDK evolves.

## 🔖 1.0

- `@Faceted` annotation marking a class for compile-time projection processing
- `FacetHost<T>` interface, implemented by a class's companion object to expose
  projection builders
- `bidirectionalFacet {}` DSL for declaring two-way projections
    - `hide()` — remove a field from a projection
    - `map()` — transform a field's value between the domain model and the
      projection
    - `rename()` — give a field a different name in a projection
- `facet-core` module — DSL and `@Faceted` annotation
- `facet-ksp` module — KSP processor generating projection code at compile time
- Gradle setup via the KSP plugin (`com.google.devtools.ksp`)

## ⏳ Later plans

- Input-only and output-only facets
- `validate` property operation
- Integration with Kotlin Serialization
    - Serializable facet
    - `renameSerial` property operation
- Framework and library integrations
    - Ktor
    - Exposed
    - Spring Boot
    - SQLDelight
    - GraphQL
    - jOOQ
