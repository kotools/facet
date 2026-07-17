# 🔂 Declarations lifecycle

## 🤔 Stability stages

This project provides different types of declaration:

- **Experimental** declarations that can be updated or removed freely from the
  Application Programming Interface (API), even by introducing incompatible
  changes. These declarations are marked with an experimental annotation
  requiring an explicit opt-in.
- **Stable** declarations that can be used safely, even in most conservative
  scenarios, and that follow strictly our [versioning strategy].
- **Deprecated** declarations that is not recommended to use and that will be
  removed in the next **major** release from the API. These declarations are
  marked with the `@Deprecated` annotation from Kotlin.

## 🧬 Evolution principles

### 🧪 Experimentation

A new declaration must be introduced in **experimental** stage for collecting
user feedbacks. This change can be included in any type of release.

### ⚖️ Stabilization

For being promoted to **stable**, an **experimental** declaration must meet the
following requirements:

- It was introduced in or before the latest **minor** release preceding the
  current version. For example, an **experimental** declaration introduced in
  version `1.0` can be stabilized in or after version `1.1`.
- It doesn't use another **experimental** declaration.

Stabilizing a declaration must be included in a **minor** or **major** release.

### 🗑️ Deprecation

A **stable** declaration must be removed incrementally by addressing the
following steps:

1. Deprecate it with a **warning** in a **minor** release.
2. Deprecate it with an **error** in a **minor** release.
3. **Hide** it from code in a **minor** release.
4. **Remove** it from code in a **major** release.

### 🔄 Matrix

| Stability stage      | Version     | Example |
|----------------------|-------------|---------|
| Experimental         | `X.Y.Z`     | `1.0.0` |
| Stable               | `X.(Y+1).0` | `1.1.0` |
| Deprecated (warning) | `X.(Y+2).0` | `1.2.0` |
| Deprecated (error)   | `X.(Y+3).0` | `1.3.0` |
| Hidden               | `X.(Y+4).0` | `1.4.0` |
| Removed              | `(X+1).0.0` | `2.0.0` |

<!----------------------------------- Links ----------------------------------->

[versioning strategy]: versioning-strategy.md
