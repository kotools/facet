# 💎 Kotools Facet

![Status: Early Development][badge-status]

> One model, many facets.

Kotools Facet is a Kotlin SDK that lets you define a faceted class once and
project it across every layer of your application.

## 😩 Problem

In a typical Kotlin project, a single concept needs a parallel data structure to
communicate with external systems. For example, representing a user accessible
via HTTP that needs persistence would look like this:

```kotlin
data class UserDto(val email: String) {
    fun toUser(): User = User(email)
}

data class User(val email: String) {
    fun toUserDto(): UserDto = UserDto(email)
    fun toUserEntity(): UserEntity = UserEntity(email)
}

data class UserEntity(val email: String) {
    fun toUser(): User = User(email)
}
```

This pattern leads to:

- **Boilerplate code**: Redundant data classes and mappers.
- **Maintenance burden**: A single property change ripples through every layer.

## 💡 Solution

With Kotools Facet, the faceted class is the only model. Declare each facet in
it, and this SDK takes care of the rest at compile-time.

```kotlin
@Faceted
data class User(val email: String) {
    object Dto : Facet<User>
    object Entity : Facet<User>
}
```

This solution provides several benefits:

- **Single source of truth**: `User` is declared once. No parallel data classes
  and mappers to maintain.
- **Easy maintenance**: Changing one property in `User` propagates across
  facets.

> [!NOTE]
> Kotools Facet is not just another mapper generator. Classic mapper generators
> answer _"How do I convert A to B?"_. Kotools Facet answers _"Why do I need B
> at all?"_.

## ✨ Features

- Mark faceted classes with `@Faceted` annotation. Supports public top-level
  data classes, with a public primary constructor containing read-only
  properties. These constructor properties can use Kotlin built-in types,
  imported types, nullable types, and generic types.
- Declare facets using `Facet` interface. Supports public nested objects.
- Generate projections at compile-time using KSP.
- Supports Kotlin/JVM platform.

## 📦 Modules

Kotools Facet ships following modules:

- `facet-dsl` that provides `@Faceted` and DSL for declaring facets.
- `facet-ksp` that generates projections at compile-time using Kotlin Symbol
  Processing (KSP).

## 🛠️ Setup

When released, setup will require a KSP plugin and the modules for your stack:

```kotlin
// In build.gradle.kts file:

plugins {
    id("com.google.devtools.ksp") version "<ksp-version>"
}

dependencies {
    ksp("org.kotools:facet-ksp:<kotools-facet-version>")
    implementation("org.kotools:facet-dsl:<kotools-facet-version>")
}
```

## 📚 Additional Documentation

- [Glossary]: Vocabulary used across this project's documentation.

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
