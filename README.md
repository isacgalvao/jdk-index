# jdk-index

Static package catalog for [`jdk`](https://github.com/isacgalvao/jdk), the
Windows-first Java version manager.

> **Generated automatically — do not edit by hand.** Every file here is
> produced by the `jdk-index-gen` tool in the main repository and force-kept
> in sync by a daily GitHub Action. Manual edits are overwritten on the next
> run.

## Layout

```
index.json                   table of contents: schema version, timestamp,
                             one entry (path/vendor/os/arch/size/sha256)
                             per platform file
windows-x64/<vendor>.json    installable packages for windows/x64
windows-aarch64/<vendor>.json  best-effort second platform, present only
                               for vendors that publish aarch64 builds
```

Each package records the tool (`java`), canonical vendor id, Java version,
os/arch, GA/EA status, LTS flag, archive size, a **mandatory sha256** and the
**direct vendor download URL** (never an ephemeral redirect). The normative
schema lives in the main repository at `crates/jdk-core/src/index.rs` — the
generator and the client share those types by construction.

Checksums come from the vendor when one is published (foojay inline value or
the vendor's own `.sha256` file); for vendors that publish none (corretto,
liberica), the generator downloads each archive once, hashes it, and reuses
that pinned hash on every later run — so early snapshots may carry only the
newest versions of those vendors while the backfill completes.

## Cadence

Regenerated daily (and on demand) by the `index` workflow of the main
repository. A failed generation opens an issue there instead of failing
silently.

## Licensing

The data files in this repository are generated metadata with no independent
license. The JDK archives they point to are the vendors' own artifacts and
carry each vendor's license (Temurin, Zulu, Corretto, Liberica, Oracle
GraalVM, Microsoft OpenJDK) — installing a JDK means accepting the license
of its vendor.
