{{/* Adapted from TauCetiReview's rubrics/correctness.md (Apache-2.0); see README.md. */ -}}
## Angle 1: Correctness and faithfulness

Your job is whether the statements say what they should. The kernel checks
proofs; it does not tell you whether a definition captures the intended
object or a theorem states the intended result. This angle may `block`.

Approach every new definition and statement adversarially: try to show that
it is wrong, vacuous, or weaker than it pretends. Approve only once you have
tried and failed.

### What to hunt for

- **Mis-formalization.** The statement does not match the mathematics. Check
  the quantifiers, the direction of each implication, the objects, and the
  edge cases: dimension zero, odd dimension, a degenerate form, the trivial
  bundle, an empty or one-point space, and characteristic 2 wherever a
  statement is over a general field (alternating and skew-symmetric differ
  there).
- **Signs and conventions.** Symplectic geometry has competing conventions,
  and the atlas page records the source's, the library's and where they
  differ, in its conventions section. Mathlib, Tau Ceti and the design may
  fix a convention that differs from the source's. Check that the statement
  is right under the convention the library uses, that a translation from
  the source's convention is right, and that the docstring names the
  convention where it matters.
- **Milestones.** For a theorem whose docstring names a milestone, read that
  milestone on the atlas page. The theorem has its hypotheses and its
  conclusion, in its generality or more, up to the conventions above. If it
  is weaker or different, `ERRATA.md` must record the error as `AGENTS.md`
  says, with a counterexample for each change, unless the atlas already
  notes it; check that the error is real.
- **Content moved into hypotheses.** Hypotheses too weak for the claim, or a
  hypothesis that is the claim's real content; a new structure that turns
  later theorems into assumptions instead of consequences.
- **Vacuity.** A statement that holds trivially, a definition defeq to `True`
  or to its own restatement, a "definition" that moves the difficulty instead
  of meeting it. A simple true lemma is not vacuous; whether it is worth
  having is another angle's question.
- **Placeholders.** `True` or another trivial stand-in in a signature or as a
  structure field's type, including a field with a plausible name that is
  really an assumption.
- **Predicates with no use.** A new `Prop`-valued definition, class or
  hypothesis structure with neither a theorem that uses it nor a nontrivial
  example, in this pull request or on `main`. Its faithfulness cannot be
  tested yet: ask for the example or the use in the same pull request.
- **Assumptions that narrow the claim.** Typeclass or structural assumptions
  stronger than the mathematics needs, which quietly weaken the result.

Check each main theorem with `#print axioms` in a scratch file that you do
not commit, under `/tmp`, run with `lake env lean`: only `propext`,
`Classical.choice` and `Quot.sound` may appear.

### Errata

A pull request that adds or changes an entry in `ERRATA.md` is yours: check
that the error is real, that each change to a statement has a counterexample,
that the file has no entry for that error yet, and, for an entry marked
**Unresolved**, that its evidence holds and its routes were really tried. A pull request that only adds an unresolved entry,
and is `Part of` its issue, need not do the issue.

### Missing prerequisites

If the pull request needs something that does not exist and fakes it, by
assuming it, bundling it as a hypothesis or using a weaker stand-in, that is
a fault. Ask for the real prerequisite in the pull request if it fits there
(one topic, within the size limit); otherwise `block`, say what it is, and
that it must come first as its own work.

### Verdict

- `block` on a mis-formalized, vacuous or placeholder statement; content
  moved into hypotheses; a milestone weaker than or different from the
  atlas's with no record of the error as `AGENTS.md` asks; a faked
  prerequisite that does not fit in the pull request; or an entry in
  `ERRATA.md` whose error is not real or is already recorded. When blocking on doubt, name the
  statement, the suspected mismatch, and the check or source that failed to
  settle it.
- `request changes` for a missing convention in a docstring, a predicate
  with no use, a prerequisite to build in the pull request, or an
  assumption that narrows the claim.
- Approve only once you have tried to break every new statement and
  definition and failed.
