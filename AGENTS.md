## Cubacadabra documentation authority

- Keep hand-written, cross-repository Cubacadabra product documentation in the
  sibling `docs` repository. Read and update its canonical contract whenever a
  public or cross-repository contract changes, in the same piece of work.
- Do not create competing hand-written contract pages in an implementation
  repository's `docs/` directory. Keep local build, test, release, and
  implementation-specific instructions in its README or CONTRIBUTING file;
  generated references stay with their generators, and executable fixtures
  stay under tests.
- Do not delete or empty existing sibling `docs/` directories until the
  central source-disposition ledger is complete and the owner explicitly
  authorizes source cleanup.

## Cross-repository architecture

Cubacadabra is one platform split across repositories. Before changing a
shared or public boundary, locate the sibling `docs` repository in the
multi-repository checkout root and read `docs/repos/<repo>/README.md` plus the
relevant current contract, system, and quality documentation.

Respect repository ownership:

- `rust` owns portable runtime, simulation, rendering-facing semantics, Luau
  execution, client-session behavior, typed contracts, and shared application
  behavior.
- Player hosts (`web`, `ios_app`, `android_app`, `desktop`) own presentation,
  credentials, transport adapters, device APIs, and OS integration.
- `tools` owns project/package construction, validation, and creator tooling.
- `studio` owns creator/editor workflows and preview integration; it must not
  invent a second interpretation of runtime or package validity.
- `backend` owns identity, routing, storage, package delivery, and
  service-side validation.
- Game-specific rules and nouns belong in game Luau rather than the shared
  runtime.
- `docs` owns hand-written cross-repository product documentation.

Do not solve a local problem by duplicating shared semantics in a host or by
moving host-specific or game-specific behavior into the shared runtime.

## Shared Rust runtime safety

The sibling `rust` repository is consumed by Studio, Web/WASM, iOS, Android,
and Desktop.

When changing shared Rust behavior:

- Treat unaffected hosts and their performance as protected.
- Prefer target/feature-gated host-specific code over changing shared default
  paths when the behavior is not genuinely portable.
- Avoid adding unnecessary per-frame work, initialization, dependencies, or
  state to every host to solve a problem for one host.
- Search sibling consumers before changing shared APIs, FFI/JNI/C bridges,
  serialized structures, loaders, feature defaults, or runtime semantics.

## Cross-repository contract changes

When changing a public/shared API, package format, schema, network message,
asset format, runtime contract, SDK API, or persisted representation:

- Search sibling repositories for producers and consumers before editing.
- Update affected producers, consumers, canonical docs, and compatibility
  evidence as one coherent change whenever practical.
- Do not leave a second hard-coded definition when an existing shared
  definition can own the contract.
- If an affected target cannot be updated or verified, state that explicitly
  rather than assuming another target proves compatibility.

## Compatibility and versioning

- Service/network changes consumed by existing clients should remain backward
  compatible unless the work explicitly includes a coordinated breaking
  version or migration.
- Keep package-format, SDK, protocol, and binary-schema versions explicit and
  independent where the canonical contracts define them separately.
- Never silently reinterpret an unknown or unsupported schema or version.
- Treat content-addressed runtime assets as immutable. Changed bytes require a
  new content identity rather than overwriting an existing published hash.
- Contract/version changes must update the canonical docs and relevant
  compatibility/conformance checks in the same piece of work.

## Verification

Use the narrowest verification that exercises the boundary actually changed.

- A successful compile proves compilation, not host behavior.
- A Rust unit test does not prove a Swift, Kotlin, JavaScript/WASM, FFI, JNI,
  loader, cache, lifecycle, or release path.
- Shared runtime, package, and protocol changes should exercise the relevant
  real host boundaries that are locally available.
- Builder/package changes should verify built output, not only source
  validators.
- If a platform, toolchain, or device is unavailable, report exactly what was
  not verified rather than claiming full cross-platform success.

## Generated artifacts and production safety

- Do not hand-edit generated or content-addressed runtime output when the
  source or generator can be changed and the artifact regenerated.
- Do not deploy, publish, apply remote migrations, overwrite remote assets, or
  modify production services unless the user explicitly requests a production
  operation.
- Follow repository-local instructions for local fixtures, emulators,
  development buckets, and test services.

## Repository-local instructions

Repository `AGENTS.md` files should contain stronger local constraints such as
language choices, build commands, UI conventions, platform tooling, and
workflow preferences. They may specialize these rules but should not redefine
the cross-repository architecture or canonical contracts.
