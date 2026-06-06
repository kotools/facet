# 🫀 Core API

The `facet-core` module provides the following API:

- [`@ExperimentalKotoolsFacetApi`](#experimentalkotoolsfacetapi-annotation)
  annotation indicating that a declaration is part of the experimental API.
- [`@Facet`](#facet-annotation) annotation indicating that a class has many
  facets.
- [`FacetHost<T>`](#facethost-interface) interface providing access to facet
  definitions.

## `@ExperimentalKotoolsFacetApi` annotation

The `@ExperimentalKotoolsFacetApi` annotation indicates that the marked
declaration is **experimental**, and can be changed incompatibly without notice.

## `@Facet` annotation

> **EXPERIMENTAL:** This declaration is not stable yet.

The `@Facet` annotation indicates that the marked class has many facets. It can
be used on classes, but not on interfaces and objects.

```kotlin
@Facet
data class User(val id: UUID, val email: String)
```

A class marked by this annotation must have a companion object implementing
[`FacetHost<T>`](#facethost-interface).

## `FacetHost` interface

> **EXPERIMENTAL:** This declaration is not stable yet.

The `FacetHost<T>` interface provides access to facet definitions. It must be
implemented by the `companion object` of the class `T`, marked by
[`@Facet`](#facet-annotation).

```kotlin
@Facet
data class User(val id: UUID, val email: String) {
    companion object : FacetHost<User>
}
```
