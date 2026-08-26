# 📖 Terminology

Kotools Facet introduces its own vocabulary for describing the relationship
between a class and its projections. This page is the canonical reference for
that vocabulary, so other documentation, decisions, and articles can rely on
these terms instead of redefining them.

## 🧩 Terms

- **Faceted class**: a class declaration annotated with `@Faceted`.
- **Facet**: a projection of a faceted class.
- **Domain value**: the value of a property as declared in the faceted class.
- **Facet value**: the value of a property as declared in a facet.
- **Bidirectional facet**: a facet that can project a faceted class instance
  into another representation, and reconstruct the faceted class instance from
  that representation.
- **Domain-facet property**: a property that exists both in a faceted class and
  in one of its facets, and that converts values in both directions.
- **Facet-only property**: a property that exists only in a facet. It produces
  its facet value but cannot reconstruct a domain value.
- **Domain-only property**: a property that exists only in a faceted class,
  excluded from a facet. It reconstructs its domain value but cannot produce a
  facet value.
