# 🗺️ Roadmap

This roadmap outlines what's planned for Kotools Facet, starting with the first
stable release. It reflects current thinking and priorities, not a committed
timeline — plans may shift as the SDK evolves.

## 🔖 1.0

- DSL for facet declarations (`facet-core-dsl` module)
    - `@Faceted` annotation marking a class for compile-time projection
      processing
    - `FacetHost<T>` interface, implemented by a class's companion object to
      expose projection builders
    - `bidirectionalFacet` function declaring two-way projections
    - `show` function adding a property to the projection
    - `hide` function removing a property from the projection
    - `rename` function renaming a property in the projection
    - `map` function transforming a property's in the projection
    - `recode` function renaming a property and transforming its value in the
      projection (`rename` + `map`)
- KSP processor generating projection code at compile time (`facet-core-ksp`
  module)
- Kotlin/JVM platform

## 🔖 1.1

- Input-only and output-only facets

## 🔖 1.2

- Integration with Kotlin Serialization (`facet-kotlinx-serialization` module)
    - `@Serializable` facet
    - `renameSerial` property operation

## 🔖 1.3

- Integration with Ktor (`facet-ktor` module)

## 🔖 1.4

- Integration with Exposed (`facet-exposed` module)

## 🔖 1.5

- Integration with Gradle (`org.kotools.facet` plugin) — adds required
  dependencies, and provides additional integrations via extension DSL

## ⏳ Later plans

- Kotlin Multiplatform (Common + JS)
- Kotlin/Native
- `validate` property operation
- Integration with Spring Boot
- Integration with SQLDelight
- Integration with GraphQL
- Integration with jOOQ
