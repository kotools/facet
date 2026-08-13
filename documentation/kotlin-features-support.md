# 🧩 Kotlin features support

This page tracks which Kotlin features the `facet-core-ksp` processor supports
for a class declaration marked by `@Faceted`.

**⏳ Not supported yet** means the feature fits the idea of Kotools Facet, a
domain type with per-layer projections, but the processor doesn't handle it yet.

**❌ Rejected** means the feature falls outside that idea: there's nothing
meaningful to project, or generated mappers couldn't reconstruct the domain
instance. See [Roadmap] for what's planned next.

## 🏛️ Class declarations

| Kotlin feature                               | Code example                                        | Status                 |
|----------------------------------------------|-----------------------------------------------------|------------------------|
| Top-level data class                         | `data class User(val id: Long)`                     | ✅ Supported since 1.0 |
| Internal data class                          | `internal data class User(val id: Long)`            | ✅ Supported since 1.0 |
| Internal primary constructor                 | `class User internal constructor(val id: Long)`     | ✅ Supported since 1.0 |
| Companion object implementing `FacetHost<T>` | `companion object : FacetHost<User>`                | ✅ Supported since 1.0 |
| Regular class                                | `class User(val id: Long)`                          | ⏳ Not supported yet   |
| Abstract class                               | `abstract class User(val id: Long)`                 | ❌ Rejected            |
| Object declaration                           | `object User`                                       | ❌ Rejected            |
| Data object declaration                      | `data object User`                                  | ❌ Rejected            |
| Annotation class                             | `annotation class User`                             | ❌ Rejected            |
| Sealed class                                 | `sealed class User`                                 | ⏳ Not supported yet   |
| Interface                                    | `interface User`                                    | ❌ Rejected            |
| Sealed interface                             | `sealed interface User`                             | ⏳ Not supported yet   |
| Enum class                                   | `enum class User { A, B }`                          | ⏳ Not supported yet   |
| Value class                                  | `@JvmInline value class Id(val value: Long)`        | ⏳ Not supported yet   |
| Generic data class                           | `data class Box<T>(val value: T)`                   | ⏳ Not supported yet   |
| Nested class                                 | `class Outer { data class User(val id: Long) }`     | ⏳ Not supported yet   |
| Local class                                  | `fun f() { data class User(val id: Long) }`         | ❌ Rejected            |
| Private or protected class                   | `private data class User(val id: Long)`             | ❌ Rejected            |
| Class without primary constructor            | `class User { constructor(id: Long) }`              | ❌ Rejected            |
| Private constructor                          | `data class User private constructor(val id: Long)` | ❌ Rejected            |

## 🧱 Constructor properties

| Kotlin feature                     | Code example                                   | Status                 |
|------------------------------------|------------------------------------------------|------------------------|
| Read-only property (`val`)         | `data class User(val id: Long)`                | ✅ Supported since 1.0 |
| Mutable property (`var`)           | `data class User(var id: Long)`                | ✅ Supported since 1.0 |
| Public property                    | `data class User(public val id: Long)`         | ✅ Supported since 1.0 |
| Internal property                  | `data class User(internal val id: Long)`       | ✅ Supported since 1.0 |
| Private or protected property      | `data class User(private val id: Long)`        | ❌ Rejected            |
| Non-property constructor parameter | `data class User(id: Long)`                    | ❌ Rejected            |
| Default parameter value            | `data class User(val page: Int = 1)`           | ⏳ Not supported yet   |
| Vararg property                    | `data class User(vararg val tags: String)`     | ⏳ Not supported yet   |
| Annotation on property             | `data class User(@Deprecated val id: Long)`    | ⏳ Not supported yet   |
| KDoc on property                   | `data class User(/** The id. */ val id: Long)` | ⏳ Not supported yet   |

## 🔤 Property types

| Kotlin feature                | Code example                         | Status                 |
|-------------------------------|--------------------------------------|------------------------|
| Nullable type                 | `val email: String?`                 | ✅ Supported since 1.0 |
| Imported type                 | `val id: java.lang.UUID`             | ✅ Supported since 1.0 |
| Generic type                  | `val tags: List<String>`             | ✅ Supported since 1.0 |
| Nested generic type           | `val data: Map<String, List<Int>>`   | ✅ Supported since 1.0 |
| Star projection               | `val items: List<*>`                 | ✅ Supported since 1.0 |
| Declaration-site variance     | `val producer: Producer<out String>` | ✅ Supported since 1.0 |
| Nullable type argument        | `val tags: List<String?>`            | ✅ Supported since 1.0 |
| Type alias                    | `typealias Id = Long`                | ⏳ Not supported yet   |
| Function type                 | `val onClick: () -> Unit`            | ⏳ Not supported yet   |
| Nullable function type        | `val onClick: (() -> Unit)?`         | ⏳ Not supported yet   |
| Multi-parameter function type | `val onMove: (Int, Int) -> Unit`     | ⏳ Not supported yet   |
| Suspend function type         | `val onSync: suspend () -> Unit`     | ⏳ Not supported yet   |
| Function type with receiver   | `val onClick: String.() -> Unit`     | ⏳ Not supported yet   |
| Definitely non-null type      | `val value: T & Any`                 | ⏳ Not supported yet   |
| Type parameter                | `val value: T`                       | ⏳ Not supported yet   |

## 🧰 Class body members

| Kotlin feature                   | Code example                                | Status               |
|----------------------------------|---------------------------------------------|----------------------|
| Body property with custom getter | `val fullName get() = "$first $last"`       | ⏳ Not supported yet |
| Delegated property               | `val lazy by lazy { compute() }`            | ❌ Rejected          |
| Secondary constructor            | `constructor(name: String) : this(0, name)` | ❌ Rejected          |
| Member function                  | `fun greet(): String = "Hi, $name"`         | ❌ Rejected          |

## 🗺️ What's next

See [Roadmap] for planned work, such as input-only and output-only facets. Every
`⏳ Not supported yet` row is a candidate for a future release. Found a feature
missing here, or one that should move from ❌ to ⏳? [Open an issue].

<!----------------------------------- Links ----------------------------------->

[Open an issue]: https://github.com/kotools/facet/issues
[Roadmap]: ../ROADMAP.md
