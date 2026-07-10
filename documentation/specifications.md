# 📑 Specifications

## 1 - `@Faceted` annotation

```kotlin
@Target(AnnotationTarget.CLASS)
annotation class Faceted
```

- A declaration annotated with `@Faceted` is referred to as a
  _faceted declaration_.
- A _faceted declaration_ MUST be top-level.
- A _faceted declaration_ MUST be public.
- A _faceted declaration_ MUST be a data class.
- A _faceted declaration_ that respects rules above is referred to as a
  _faceted class_.

## 2 - `FacetHost` interface

```kotlin
interface FacetHost<T : Any>
```

- The `T` type parameter of `FacetHost` MUST be a subtype of `Any`.
- A _faceted class_ MUST have a companion object.
- The companion object of a _faceted class_ MUST be public.
- The companion object of a _faceted class_ MUST implement `FacetHost`.
- The companion object of a _faceted class_ MUST implement `FacetHost<T>`, where
  `T` is the _faceted class_.
