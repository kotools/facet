# 💎 Kotools Facet

![Status: Early Development][badge-status]

> One model, many facets.

Kotools Facet is a Kotlin SDK that lets you define a faceted class once and
project it across every layer of your application.

## 😩 Problem

In a typical Kotlin project, a single concept needs a parallel data structure to
communicate with external systems. For example, representing a user accessible
via HTTP would look like this:

```kotlin
data class User(val id: UUID, val email: String, val password: String) {
    fun toUserResponse(): UserResponse = UserResponse(
        id = this.id.toString(),
        email = this.email,
        name = this.email.substringBefore('@')
    )
}

data class UserResponse(val id: String, val email: String, val name: String)
```

This pattern leads to:

- **Boilerplate code**: Redundant data classes and mappers.
- **Maintenance burden**: A single property change ripples through every layer.

## ✨ Solution

With Kotools Facet, the faceted class is the only model. Declare each facet in
it, and this SDK takes care of the rest at compile-time.

```kotlin
@Faceted
data class User(val id: UUID, val email: String, val password: String) {
    object Response : OutgoingFacet<User>() {
        val id = map { it.id.toString() }
        val password = hide()
        val name = compute { it.email.substringBefore('@') }
    }
}
```

This solution provides several benefits:

- **Single source of truth**: `User` is declared once. No parallel data classes
  and mappers to maintain.
- **Easy maintenance**: Changing one property in `User` propagates across
  facets.

> [!NOTE]
> Kotools Facet is not just another mapper generator.
>
> Classic mapper generators answer _"How do I convert A to B?"_. They require
> `UserDto` and `UserEntity` to exist.
>
> Kotools Facet answers _"Why do I need B at all?"_. It requires only the
> faceted class (`User`).

## 📦 Modules

Kotools Facet ships following modules:

- `facet-core-dsl` that provides `@Faceted` and DSL for declaring facets.
- `facet-core-ksp` that generates projections at compile-time.

## 🛠️ Setup

When released, setup will require a KSP plugin and the modules for your stack:

```kotlin
// In build.gradle.kts file:

plugins {
    id("com.google.devtools.ksp") version "<ksp-version>"
}

dependencies {
    ksp("org.kotools:facet-core-ksp:<facet-version>")
    implementation("org.kotools:facet-core-dsl:<facet-version>")
}
```

## 📚 Additional Documentation

- [Glossary]: Vocabulary used across this project's documentation.
- [Kotlin features support]: Supported and unsupported Kotlin features.
- [Roadmap]: What's planned next.

## 📬 Get Early Access

Kotools Facet is commercial software. To get notified when it ships and to
discuss licensing, **join the waiting list** by sending an email to
[contact@kotools.org] with the subject **"Kotools Facet – Waiting List"**.

## 📄 License

The SDK modules are distributed under a commercial license. To enquire about
licensing, contact us at [contact@kotools.org].

<!----------------------------------- LINKS ----------------------------------->

[badge-status]: https://img.shields.io/badge/Status-Early%20Development-orange.svg
[contact@kotools.org]: mailto:contact@kotools.org
[glossary]: documentation/glossary.md
[kotlin features support]: documentation/kotlin-features-support.md
[roadmap]: documentation/roadmap.md
