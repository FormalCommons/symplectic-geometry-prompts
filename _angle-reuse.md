{{/* Adapted from TauCetiReview's rubrics/reuse.md (Apache-2.0); see README.md. */ -}}
## Angle 2: Reuse and duplication

The pull request must not duplicate what Mathlib, Tau Ceti or this library
already has, directly or through thin wrappers. Where existing theory can be
used, it must be. A new declaration that an existing one directly replaces is
a `block`; every other kind of duplication below is `request changes`.

### Where to look

Mathlib's sources are under `.lake/packages/mathlib/Mathlib`, Tau Ceti's under
`.lake/packages/TauCeti/TauCeti`, this library's under `SymplecticGeometry/`.
Tau Ceti already has much linear algebra and geometry; search it as hard as
Mathlib. The atlas page that the pull request serves, at `/atlas/atlas/`,
ends with a correspondence list that names existing Mathlib and Tau Ceti
declarations: check every one that touches the pull request. Also look at
the open pull requests (`gh pr list`) for the same material in flight.

### Searches to run

Choose search terms and grep to verify.

- For each new declaration, an existing one with the same content. It may
  have another name than you expect, or match up to renaming, unfolding,
  symmetry or duality, or through an existing bridging lemma.
- For each proof more than a few lines long, its goal and its key
  intermediate steps. Standard plumbing (bilinear forms and matrices, bases
  and `Fin` sums, submodule and orthogonal-complement computations) almost
  always has a named lemma; keep searching until you find it or are
  confident it is absent.
- For each definition assembled from raw pieces, a library construction that
  does the assembly.
- For each new block of code, this library and Tau Ceti for its distinctive
  identifiers or proof shape: near-clones should become one shared
  construction.
- Within the diff: private lemmas that restate public ones up to defeq,
  composite lemmas that their parts' `@[simp]` lemmas already prove, and
  `∧`-bundles of existing lemmas.
- Compatibility aliases, wrappers, forwarding imports, deprecated shims and
  duplicate names: unnecessary duplication; ask for their removal.

### Rejecting it

Every finding names the existing declaration that replaces the new one and
says how to use it, with a one-line example if needed, backed by your grep
hit. Do not ask the author to search. Not every hit is a defect: Mathlib keeps
per-type restatements of general lemmas, and a specialization with real uses
can earn its place.

### Verdict

- `block` on a declaration that an existing one directly replaces.
- `request changes` for results that existing ones readily prove, special
  cases, parallel APIs, and proofs, definitions or scaffolding that re-derive
  what a located lemma or construction already gives.
- Approve when the pull request adds new material and reuses existing API
  where it can.
