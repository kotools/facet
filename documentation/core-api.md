# 🫀 Core API

The `facet-core` module provides the following API:

- [`@Facet`](#facet-annotation) annotation indicating that a class has many
  facets.
- [`FacetHost<T>`](#facethost-interface) interface providing access to facet
  definitions.

## `@Facet` annotation

The `@Facet` annotation indicates that the marked class has many facets. It can
be used on classes, but not on interfaces and objects.

```kotlin
@Facet
data class User(val id: UUID, val email: String)
```

A class marked by this annotation must have a companion object implementing
[`FacetHost<T>`](#facethost-interface).

## `FacetHost` interface

The `FacetHost<T>` interface provides access to facet definitions. It must be
implemented by the companion object of the class `T`, marked by
[`@Facet`](#facet-annotation).

```kotlin
@Facet
data class User(val id: UUID, val email: String) {
    companion object : FacetHost<User>
}
```
