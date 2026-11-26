# 💎 Kotools Facet

![Status: Early Development][badge-status]

> One model, many facets.

Kotools Facet is a Kotlin SDK that removes data class duplication and mapper
boilerplate. Declare a class once, and the SDK generates projections at
compile-time.

## 😩 Problem

In a typical Kotlin project, a single concept needs a parallel data structure to
communicate with external systems (like HTTP or a database).

```kotlin
data class User(
    val id: Int,
    val email: String,
    val name: String,
    val age: Int
) {
    fun toDto(): UserDto = UserDto(id, email, name, age)
}

data class UserDto(
    val id: Int,
    val email: String,
    val name: String,
    val age: Int
)
```

This pattern leads to:

- **Boilerplate code**: Redundant data classes and mappers.
- **Maintenance burden**: A single property change must be repeated in every
  class and every mapper.

## 💡 Solution

With Kotools Facet, the _faceted class_ is the only model and holds its
perspectives (_facets_).

```kotlin
@Faceted
data class User(
    val id: Int,
    val email: String,
    val name: String,
    val age: Int
) {
    object Dto : Facet
}
```

At compile-time, each _facet_ yields a _projection_. For the `Dto` _facet_
above, the SDK generates this class and this function:

```kotlin
fun User.toDto(): UserDto = UserDto(
    id = this.id,
    email = this.email,
    name = this.name,
    age = this.age
)

data class UserDto(
    val id: Int,
    val email: String,
    val name: String,
    val age: Int
)
```

You then use it like any other Kotlin code:

```kotlin
val user = User(id = 1, email = "user@example.org", name = "User", age = 30)
println(user) // User(id=1, email=user@example.org, name=User, age=30)

val dto = user.toDto()
println(dto) // UserDto(id=1, email=user@example.org, name=User, age=30)
```

> [!NOTE]
> Generated names and functions are a design proposal. Tell us what you would
> change in the [Give Feedback](#-give-feedback) section.

See the [glossary] for the vocabulary used here.

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

## 💬 Give Feedback

Kotools Facet is in early development, and v1.0.0 is shaped by what Kotlin
developers need. Join the [discussion][feedback-discussion].

To follow the project and be notified of the first release, watch this
repository (**Watch** > **Custom** > **Discussions**).

## 📄 License

Free for non-commercial use is planned. Final terms will be published with the
first release. To enquire about commercial licensing, contact us at
[contact@kotools.org].

<!----------------------------------- LINKS ----------------------------------->

[badge-status]: https://img.shields.io/badge/Status-Early%20Development-orange.svg
[contact@kotools.org]: mailto:contact@kotools.org
[feedback-discussion]: https://github.com/kotools/facet/discussions/6
[glossary]: GLOSSARY.md
