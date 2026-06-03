# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with
code in this repository.

## Project Overview

Kotools Facet is a Kotlin SDK that lets you define your domain model once and
project it across every layer of your application (HTTP, persistence, and
beyond) without writing mappers. It uses compile-time annotation processing and
a declarative DSL.

The core API looks like this:

```kotlin
@Faceted
data class User(val id: UUID, val email: String) {
    companion object : FacetScope<User> {
        val http = ktorFacet {
            request { User::id.hide(seed = UUID::randomUUID) }
            response { User::id.map(UUID::toString) }
        }
        val database = exposedFacet {
            User::id.map(name = "user_id", transform = UUID::toString)
            User::email.map(name = "user_email")
        }
    }
}
```

## Licensing

The repository itself is MIT-licensed. The SDK modules are distributed under a
commercial license.

## Git

Never create commits. Stage changes if needed, but leave committing to the
developer.

## Code Style

Enforced via `.editorconfig`:
- Max line length: **80 characters** (visual guides at 80 and 90)
- Charset: UTF-8, line endings: LF
- Continuation indent: 8 spaces
