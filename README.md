# 💎 Kotools Facet

![Status: Early Development][badge-status]

> One model, many facets.

Kotools Facet is a Kotlin SDK that lets you define your domain model once and
project it across every layer of your application — HTTP, persistence, and
beyond — without writing a single mapper.

## 😩 The Problem

In a typical Kotlin backend, a single concept like `User` needs a parallel data
structure to be persisted:

```kotlin
// ------------------------------ Data structures ------------------------------

// Domain
data class User(val id: UUID, val email: String)

// Persistence
data class UserEntity(val id: String, val email: String)

// ---------------------------------- Mappers ----------------------------------

// Persistence
fun User.toEntity(): UserEntity = UserEntity(id.toString(), email)
fun UserEntity.toUser(): User = User(UUID.fromString(id), email)
```

This pattern leads to:

- **Boilerplate code** — mappers, extension functions, and redundant data
  classes
- **Scattered logic** — business rules spread across layers instead of living on
  the domain
- **Maintenance burden** — a single field change ripples through every layer

## ✨ The Solution

With Kotools Facet, your domain model is the only model. Declare how each layer
should see it, and Kotools Facet takes care of the rest at compile time.

```kotlin
@Faceted
data class User(val id: UUID, val email: String) {
    companion object : FacetHost<User> {
        val entity: BidirectionalFacet<User> = bidirectionalFacet {
            map(
                User::id,
                transformInput = { UUID.fromString(it) },
                transformOutput = { it.toString() }
            )
        }
    }
}
```

The `companion object` is the projection registry for `User` — no separate class
or configuration file required.

- `@Faceted` marks the class for compile-time projection processing.
- `FacetHost<T>` is implemented by the companion object to expose projection
  builders for each layer.
- Within `bidirectionalFacet {}`, `hide()` removes a field from a projection;
  `map()` transforms it; `rename()` gives it a different name in the projection.

This solution provides several benefits:

- **Single source of truth** — `User` is declared once; every layer reads from
  it. No parallel `UserEntity` or `UserHttpResponse` classes.
- **Domain-first** — `hide()` and `map()` live on `User` itself, not in a
  service or mapper. Business rules stay with the model.
- **No mappers** — `bidirectionalFacet {}` declares projections; the SDK
  generates the glue at compile time.
- **Less boilerplate** — no `UserHttpRequest` or `UserHttpResponse` classes; no
  mapper functions to maintain.

## 📦 Modules

Kotools Facet currently ships the following modules:

| Module       | What it does                                                  |
|--------------|---------------------------------------------------------------|
| `facet-core` | DSL and `@Faceted` annotation — required by all other modules |
| `facet-ksp`  | KSP processor — generates projection code at compile time     |

See [roadmap] for what's planned next.

## 🚀 Getting Started

> **Note:** Kotools Facet is currently in early development. Installation
> instructions, full API documentation, and migration guides will be published
> here upon the first stable release.

When released, setup will require a KSP plugin and the modules for your stack:

```kotlin
// build.gradle.kts
plugins {
    id("com.google.devtools.ksp") version "<ksp-version>"
}

dependencies {
    ksp("org.kotools:facet-ksp:<facet-version>")
    implementation("org.kotools:facet-core:<facet-version>")
}
```

## 📬 Get Early Access

Kotools Facet is commercial software. To get notified when it ships and to
discuss licensing, **join the waiting list** by sending an email to
[contact@kotools.org] with the subject **"Kotools Facet – Waiting List"**.

## 📄 License

The SDK modules are distributed under a commercial license. To enquire about
licensing, contact us at [contact@kotools.org].

<!----------------------------------- Links ----------------------------------->

[badge-status]: https://img.shields.io/badge/Status-Early%20Development-orange.svg
[contact@kotools.org]: mailto:contact@kotools.org
[roadmap]: ./ROADMAP.md
