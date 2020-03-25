# API Management

> Guidance below for Theia framework. End products will get better development experience by using private visibility.

Theia is a framework embracing openness, extensibility, and customizability as much as possible:
- API defaults to public for clients.
- API defaults to protected for extenders.
- Language constructions prohibiting runtime access to internals are never used and so on.

Usually, the version management is built around API visibility.
Particularly, if a public API is broken then the major release is required.

Following the conventional approach is not practicable for Theia since all APIs are more or less public.
It will slow down API innovation, accumulate technical debt or require many major releases.

Instead, we require the major release only if a stable API is broken.
Breaking an experimental API can be done with the minor release,
but not necessary if such API does not have sufficient adoption.

## Stability

Conceptually, an API is all assumptions adopters depend on to make use or extend Theia.
A stable API is based on assumptions that are not subject to change.
It does not matter whether an API is public or internal, or whether it is used a lot or never.

> For instance, the language server protocol depends on such data types like URIs and positions
since they don't change from language to language. It ensures its stability.

The API stability indicated by adding, exclusively, `@experimental` or `@stable` js-doc tags.
An API without a stability tag considered to be experimental.

### Experimental

- All new APIs should always be added as `experimental`
since it's almost impossible to get stable API right first time.
- Usually, experimental APIs don't require the stability tag,
but if a new member is added to `stable` API then it should be explicitly annotated.
- Such APIs should not have extensive documentation to avoid the maintenance burden.
- They can be changed or removed without the deprecation cycle if it was not widely adopted.
- Adoption should be measured by the number of internal clients or based on the feedback of Theia contributors and committers.

### Stable

- Experimental APIs can be graduated to `stable` after at least one major release.
- Such experimental APIs must not be based on design decisions that will likely change
and must have sufficient adoption.
- Stable APIs should have proper documentation.
Low maintenance effort is ensured by their stability.
- They can be changed only in a backward-compatible fashion.
- They can be removed only via the deprecation cycle.

## Deprecation

Deprecated *stable* API can be removed after at least one *major* release.

Deprecated *experimental* API can be removed after at least one *minor* release.

Breaking changes should be documented in CHANGELOG. Each breaking change should be justified to adopters
and guide what should be done instead.
