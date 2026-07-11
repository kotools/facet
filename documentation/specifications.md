# 📑 Specifications

## Introduction

Each rule in this document is expressed using an [RFC 2119] keyword. KSP
processor maps these keywords to a log severity as follows:

| Keyword             | Severity      | Compilation outcome  |
|---------------------|---------------|----------------------|
| MUST / MUST NOT     | Error         | Compilation fails    |
| SHOULD / SHOULD NOT | Warning       | Compilation proceeds |
| MAY                 | No diagnostic | Not a violable rule  |

A MUST violation indicates the generated code would be incoherent or unsafe; the
processor reports it as an error and fails compilation.

A SHOULD violation is a recommendation; the processor reports it but continues
processing.

The MAY keyword describes a valid possibility, not a constraint — it has no
violation and therefore produces no diagnostic.

## `@Faceted` annotation

```kotlin
@Target(AnnotationTarget.CLASS)
annotation class Faceted
```

- A declaration annotated with `@Faceted` is referred to as a
  _faceted declaration_.
- A _faceted declaration_ MUST be top-level.
- A _faceted declaration_ MUST be public or internal.
- A _faceted declaration_ MUST be a data class.
- A _faceted declaration_ that respects requirements above is referred to as a
  _faceted class_.
- A _faceted class_ SHOULD have a companion object.
- The companion object of a _faceted class_ MUST be public or internal.

## `FacetHost` interface

```kotlin
interface FacetHost<T : Any>
```

- A _faceted class_ MUST NOT implement `FacetHost`.
- The companion object of a _faceted class_ SHOULD implement `FacetHost`.
- If the companion object of a _faceted class_ implements `FacetHost<T>`, the
  `T` type parameter MUST be the _faceted class_ itself.
- Class declarations nested in a _faceted class_, except its companion object,
  MUST NOT implement `FacetHost`.

<!----------------------------------- Links ----------------------------------->

[RFC 2119]: https://datatracker.ietf.org/doc/html/rfc2119
