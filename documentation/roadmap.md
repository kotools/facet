# 🗺️ Roadmap

This roadmap outlines what's planned for Kotools Facet. It reflects current
thinking and priorities, not a committed timeline. Plans may shift as the SDK
evolves.

## 🔖 v1.0

- Kotlin/JVM platform.
- DSL for facet declarations (`facet-core-dsl` module):
    - `@Faceted` annotation that enables compile-time facet processing.
    - `OutgoingFacet` interface that declares a facet with a _projecting_ mapper
      only. It supports these property operations:
        - `map` that transforms a faceted property's type.
        - `hide` that excludes a faceted property from a projection.
        - `compute` that declares a projected property computed from the faceted
          class.
- KSP processor generating projections at compile-time (`facet-core-ksp`
  module).

## 🔖 v1.1

`IncomingFacet` interface that declares a facet with a _faceting_ mapper only.
It supports `map` and `hide` property operations.

## 🔖 v1.2

`BidirectionalFacet` interface that declares a bidirectional facet, with
_faceting_ and _projecting_ mappers. It supports `map`, `hide` and `compute`
property operations.

## ⏳ Later plans

- `rename` property operation that renames a faceted property without changing
  its type + `@FacetPropertySource` annotation that associates the projected
  property with the faceted one.
- `validate(property, predicate)` property operation that checks the validity of
  a `property` against a `predicate`. The processor generates a pair of mappers
  that throw an exception or return `null` in case of invalid `property`.
- `mutable(property)` property operation that makes a projected property
  mutable.
- Integration with Kotlin Serialization (`facet-serialization` DSL and KSP
  modules). 2 options:
    1. Propagating `@Serializable` and `@SerialName` annotations from facets to
       projections.
    2. Introducing `SerializableFacet` interface to declare a serializable
       facet, and `renameSerial` property operation to set the serial name of a
       projected property.
- Kotlin Multiplatform (Common + JS + Native).
- Integration with Ktor (`facet-ktor` DSL and KSP modules).
- Integration with Exposed (`facet-exposed` DSL and KSP modules).
- Integration with Gradle (`org.kotools.facet` plugin): adds required
  dependencies, and provides additional integrations via extension DSL.
- Integration with Spring Boot.
- Integration with SQLDelight.
- Integration with GraphQL.
- Integration with JOOQ (Java Object-Oriented Querying).
