{{/* Adapted from TauCetiReview's rubrics/api-design.md, generality.md, placement.md, naming.md, documentation.md and proof-quality.md (Apache-2.0); see README.md. */ -}}
## Angle 4: Library quality

Is this good library code, which others can use and which could move to Tau
Ceti or Mathlib with little more than a new namespace? Use `request changes`,
never `block`. `AGENTS.md` sets the library's rules; judge by them.

### Public API

- Judge the interface as it stands after the pull request; ask for the
  removal of any compatibility-only surface.
- Under-exposure is a finding: a result whose statement mentions only Mathlib
  or Tau Ceti types and whose proof does not depend on this file's subject is
  general infrastructure. It belongs, public, in its natural home, not
  `private` here. `private` is for a step of one proof.
- A definition comes with the API that characterizes it: how to build and use
  it, the `foo_def` and `mem_foo_iff` restatements (`foo_def := (rfl)`, not
  `:= rfl`), its interaction with the operations around it, and its
  universal property if it has one. Try to use the new API without unfolding,
  and ask for each missing lemma.
- A bundled definition must be extensional: no data that its laws leave free.
  If `@[ext]` cannot follow from agreement on what the operations and laws
  use, the definition carries free data; ask for its removal.
- Ask for symmetric, dual or parallel forms only when the file already
  develops both sides or the plan needs them.
- `@[simp]` on normal-form lemmas, `@[grind]` on lemmas that should drive
  `grind`. Flag a missing annotation on a characteristic lemma, and one that
  would loop or fire wrongly.

### Generality

- Flag assumptions that are unused, stronger than Mathlib's conventions, or
  contradicted by a more general theorem nearby; show the signature you
  want. A symplectic vector space over a field is often enough where the
  proof assumes `ℝ`; finite dimension is often needed only for part of a
  file.
- Prove the general result first and derive the special cases; flag a proof
  repeated for a special case.
- Generalize to the natural form, not speculatively: flag both
  under-generalization and abstraction with no use.

### Placement and imports

- Each declaration lives in its natural home: the file whose topic, level and
  dependencies fit it, near what it elaborates, as `AGENTS.md`'s layout and
  `DESIGN.md` say. If it belongs in an earlier file, or depends on no later
  theory and is broadly useful, ask for the move.
- Do not let material specific to one milestone pose as reusable by living in
  a general file, or general material hide in a milestone's file.
- When a new file would put `Foo.lean` and `FooBar.lean` side by side, they
  become `Foo/Basic.lean` and `Foo/Bar.lean` in the same pull request.
- Flag only an evidently wrong import: unused, or whole-library.

### Naming and notation

- A theorem's name describes its conclusion in Mathlib's terms
  (<https://leanprover-community.github.io/contribute/naming.html>), and
  matches the declarations next to it. If you call a term nonstandard, cite
  the Mathlib name or the source's term.
- A name never claims more than the statement: `_iff` only for an iff, `_eq`
  only for an equality.
- Material goes in the namespace `SymplecticGeometry`, except a declaration
  about an existing Lean, Mathlib or Tau Ceti type, which goes in that type's
  namespace, so that dot notation finds it and it can move upstream unchanged.
- Notation is sparing and `scoped`, following Mathlib's precedent for the
  same object.

### Documentation

- Each substantive file opens with a module docstring that says what it holds
  and why, mathematically, with its references.
- Public definitions, main theorems and instances whose purpose is not plain
  have docstrings about the object or the result, not the proof, the issue
  or the project's process.
- A docstring that promises more than the statement delivers, or is wrong or
  stale, is a finding even when the theorem is right.

### Proofs

- Prefer robust automation (`grind`, `simp`, `omega`) to long chains of
  rewriting with named lemmas, which break on renames.
- `change` and `show` need a comment saying why the goal cannot be reached
  otherwise. Flag reliance on accidental definitional equality across
  wrappers or coercions; ask for a lemma instead.
- Factor substantial or repeated reasoning into lemmas. A proof over 50 lines
  usually hides steps that should be lemmas; if it cannot be split, comments
  should explain its structure.

### Verdict

- `request changes` for a compatibility-only or over-exposed surface, general
  results hidden as `private`, an incomplete characteristic API, free data
  that defeats extensionality, wrong or missing annotations; assumptions that
  are unused or too strong, special-case duplication, the wrong level of
  generality; a declaration in the wrong home, or an evidently wrong import;
  a name that describes the proof, overstates the statement or sits in the
  wrong namespace; a missing or misleading docstring; a brittle proof, or one
  that hides reusable facts.
- Approve when the surface is minimal and complete, the statements are at
  their natural level and in their natural place, and names, documentation
  and proofs are sound.
