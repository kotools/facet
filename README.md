# 💎 Kotools Facet

![Status: Early Development][badge-status]

> One model, many facets.

Kotools Facet is a Kotlin SDK that lets you define your domain model once and
project it across every layer of your application — HTTP, persistence, and
beyond — with no mappers and no parallel classes to maintain.

## 😩 The Problem

In a typical Kotlin backend, a single concept like `User` needs a parallel data
structure to be persisted:

```kotlin
data class User(val id: UUID, val email: String)
data class UserEntity(val id: String, val email: String)

fun User.toUserEntity(): UserEntity = UserEntity(id.toString(), email)
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
        val entity: BidirectionalFacet<User> by bidirectionalFacet {
            map(
                property = User::id,
                transformOutput = { it.toString() },
                transformInput = { UUID.fromString(it) }
            )
        }
    }
}

// Generates:
// - UserEntity data class
// - User.toUserEntity() and UserEntity.toUser() extension functions
```

- The `companion object` is the projection registry for `User` — no separate
  class or configuration file required.
- `@Faceted` marks the class for compile-time projection processing.
- `FacetHost<T>` is implemented by the companion object to expose projection
  builders for each layer.
- Within `bidirectionalFacet {}`, declare the shape of the projection using
  property operations, like `map()` transforming the property's value.

This solution provides several benefits:

- **Single source of truth** — `User` is declared once; every layer reads from
  it. No parallel `UserEntity` or `UserHttpResponse` classes.
- **Domain-first** — property operations live on `User` itself, not in a service
  or mapper. Business rules stay with the model.
- **No mappers** — `bidirectionalFacet {}` declares the projection's shape;
  there's no conversion function to write or keep in sync.
- **Less boilerplate** — no `UserHttpRequest` or `UserHttpResponse` classes; no
  mapper functions to maintain.

## 🆚 Not Just Another Mapper Generator

Several KSP and compiler-plugin tools already exist to generate mappers between
two classes. They take a `UserDto` and a `UserEntity` you've already written and
eliminate the `toEntity()` / `toDto()` boilerplate between them. Kotools Facet
also runs on KSP — the difference isn't the tooling, but what problem it solves.

Instead of just generating the glue *between* separate classes, Kotools Facet
removes the need for those classes to exist in the first place. There's no
`UserDto`, no `UserEntity` — only `User`, with its projections declared as part
of the model itself.

|                 | Answers                      | Requires                |
|-----------------|------------------------------|-------------------------|
| Classic mappers | *"How do I convert A to B?"* | `UserDto`, `UserEntity` |
| Kotools Facet   | *"Why do I need B at all?"*  | Only `User`             |

## 📦 Modules

Kotools Facet currently ships the following modules:

| Module           | What it does                                          |
|------------------|-------------------------------------------------------|
| `facet-core-dsl` | DSL and annotations — required by all other modules   |
| `facet-core-ksp` | KSP processor — generates projections at compile time |

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
    ksp("org.kotools:facet-core-ksp:<facet-version>")
    implementation("org.kotools:facet-core-dsl:<facet-version>")
}
```

## 📚 Additional Documentation

- [Roadmap] — what's planned next
- [Changelog] — release history
- [Versioning strategy] — our backward-compatibility policy
- [Declarations lifecycle] — stability stages and evolution principles
- [Kotlin features support] — supported and unsupported Kotlin features

## 📬 Get Early Access

Kotools Facet is commercial software. To get notified when it ships and to
discuss licensing, **join the waiting list** by sending an email to
[contact@kotools.org] with the subject **"Kotools Facet – Waiting List"**.

## 📄 License

The SDK modules are distributed under a commercial license. To enquire about
licensing, contact us at [contact@kotools.org].

<!----------------------------------- Links ----------------------------------->

[badge-status]: https://img.shields.io/badge/Status-Early%20Development-orange.svg
[changelog]: CHANGELOG.md
[contact@kotools.org]: mailto:contact@kotools.org
[declarations lifecycle]: documentation/declarations-lifecycle.md
[kotlin features support]: documentation/kotlin-features-support.md
[roadmap]: ROADMAP.md
[versioning strategy]: documentation/versioning-strategy.md
