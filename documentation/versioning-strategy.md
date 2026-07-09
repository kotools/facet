# 🔂 Versioning strategy

For versioning the Application Programming Interfaces (APIs) of Kotools Facet,
we have a pragmatic approach based on the concept of backward compatibility.

## 🤔 Types of compatibility

We focus on three types of compatibility:

- **Behavioral compatibility** ensures that new code doesn't change the behavior
  of existing one.
- **Source compatibility** ensures that client's code recompile correctly
  against a newer version of Kotools Facet.
- **Binary compatibility** ensures that a newer version of Kotools Types can
  replace a previously compiled version of this library.

## ⚖️ Stable API

With these types of compatibility in mind, here are the different types of
release that we ship for the stable API of Kotools Facet:

- **Incremental releases (`X.Y.Z`)** that can break the **behavioral
  compatibility** for fixing bugs, but the **source compatibility** and the
  **binary compatibility** should be preserved.
- **Minor releases (`X.Y`)** that can break the **behavioral compatibility** for
  fixing bugs and the **source compatibility** for deprecating declarations, but
  the **binary compatibility** should be preserved.
- **Major releases (`X`)** that can break the **behavioral compatibility** for
  fixing bugs, the **source compatibility** for deprecating declaration, and the
  **binary compatibility** for removing declarations.

## 🧪 Experimental API

We also ship an experimental API of Kotools Facet for trying out ideas and
collecting feedbacks from users. This API includes all declarations marked with
the `ExperimentalKotoolsFacetApi` annotation requiring an explicit [opt-in].

Please note that this API doesn't have the same compatibility policy as the
stable one: _**experimental changes can break any type of compatibility in any
type of releases listed above**_!

<!----------------------------------- Links ----------------------------------->

[opt-in]: https://kotlinlang.org/docs/opt-in-requirements.html
