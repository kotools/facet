# 🗺️ Roadmap

This roadmap outlines what's planned for Kotools Facet. It reflects current
thinking and priorities, not a committed timeline. Plans may shift as the SDK
evolves.

## 🔖 0.1

- Kotlin/JVM platform.
- DSL for facet declarations (`facet-core-dsl` module):
    - `@Faceted` annotation that enables compile-time projection processing.
    - `BidirectionalFacet` interface that declares a two-way projection, with
      _facet-to-domain_ and _domain-to-facet_ mappers.
    - `InputOnlyFacet` interface that declares an input projection, with
      _facet-to-domain_ mapper only.
    - `OutputOnlyFacet` interface that declares an output projection, with
      _domain-to-facet_ mapper only.
- KSP processor generating projections at compile-time (`facet-core-ksp`
  module).

## ⏳ Later plans

- Kotlin Multiplatform (Common + JS + Native).
- `rename` function that renames a domain property without changing its type +
  `@FacetPropertySource` annotation that associates a facet property declaration
  with a property declared by the faceted class.
- `map` function that transforms a domain property's type.
- `compute` function that declares a facet property computed from the faceted
  class.
- `hide` function that excludes a domain property from a facet.
- `validate(property, predicate)` function to check the validity of a `property`
  against a `predicate`, and to generate a pair of mappers that throw an
  exception or return `null` in case of invalid `property`.
- `mutable(property)` DSL function to control the mutability independent of the
  source.
- Integration with Kotlin Serialization (`facet-serialization` DSL and KSP
  modules):
    - `@Serializable` facet
    - `renameSerial` property operation
- Integration with Ktor (`facet-ktor` DSL and KSP modules).
- Integration with Exposed (`facet-exposed` DSL and KSP modules).
- Integration with Gradle (`org.kotools.facet` plugin): adds required
  dependencies, and provides additional integrations via extension DSL.
- Integration with Spring Boot.
- Integration with SQLDelight.
- Integration with GraphQL.
- Integration with JOOQ (Java Object-Oriented Querying).
