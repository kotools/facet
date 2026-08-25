# 🗺️ Roadmap

This roadmap outlines what's planned for Kotools Facet, starting with the first
stable release. It reflects current thinking and priorities, not a committed
timeline — plans may shift as the SDK evolves.

## 🔖 1.0

- DSL for facet declarations (`facet-core-dsl` module)
    - `@Faceted` annotation marking a class for compile-time projection
      processing
    - `@FacetPropertySource` annotation that associates a facet property
      declaration with a property declared by the faceted class
    - `BidirectionalFacet` interface declaring two-way projections
    - `BidirectionalFacet.rename` function that renames a domain property
      without changing its type
    - `BidirectionalFacet.map` function that transforms a domain property's type
    - `BidirectionalFacet.compute` function that declares a facet property
      computed from the faceted class
    - `BidirectionalFacet.hide` function that excludes a domain property from a
      facet
- KSP processor generating projection code at compile time (`facet-core-ksp`
  module)
- Kotlin/JVM platform

## 🔖 1.1

- Input-only and output-only facets

## 🔖 1.2

- Integration with Kotlin Serialization (`facet-serialization` DSL and KSP
  modules)
    - `@Serializable` facet
    - `renameSerial` property operation

## 🔖 1.3

- Integration with Ktor (`facet-ktor` DSL and KSP modules)

## 🔖 1.4

- Integration with Exposed (`facet-exposed` DSL and KSP modules)

## 🔖 1.5

- Integration with Gradle (`org.kotools.facet` plugin) — adds required
  dependencies, and provides additional integrations via extension DSL

## ⏳ Later plans

- Kotlin Multiplatform (Common + JS)
- Kotlin/Native
- `validate(property, predicate)` function to check the validity of a `property`
  against a `predicate`, and to generate a pair of mappers that
  throw an exception or return `null` in case of invalid `property`
- `mutable(property)` DSL function to control the mutability independent of the
  source
- Integration with Spring Boot
- Integration with SQLDelight
- Integration with GraphQL
- Integration with jOOQ
