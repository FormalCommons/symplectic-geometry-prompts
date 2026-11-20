{{/* Adapted from TauCetiReview's rubrics/correctness.md (Apache-2.0); see README.md. */ -}}
## Angle 1: Correctness and faithfulness

Your job is whether the statements say what they should. The kernel checks
proofs and CI checks axioms; neither tells you whether a definition captures
the intended object or a theorem states the intended result. This angle may
`block`.

Approach every new definition and statement adversarially: try to show that
it is wrong, vacuous, or weaker than it pretends. Approve only once you have
tried and failed.

### What to hunt for

- **Mis-formalization.** The statement does not match the mathematics. Check
  the quantifiers, the direction of each implication, the objects, and the
  edge cases: dimension zero, odd dimension, a degenerate form, the trivial
  bundle, an empty or one-point space.
- **Signs and conventions.** Symplectic geometry has competing conventions:
  the sign of the standard form, of `J₀`, of `ω(·, J·)`, of the Hamiltonian
  vector field, of the Maslov index. Check each against the conventions of
  the atlas page it serves, at `/atlas/atlas/`, and the auxiliary pages it
  points to. A theorem true only under another convention is wrong here.
- **Milestones.** For a theorem whose docstring names a milestone, read that
  milestone on the atlas page. The theorem has its hypotheses and its
  conclusion, in its generality or more. If it is weaker or different,
  `ERRATA.md` must have an entry for it in the same pull request, with a
  counterexample for each change; check that the error is real.
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
not commit, run with `lake env lean`: only `propext`, `Classical.choice` and
`Quot.sound` may appear.

### Missing prerequisites

If the pull request needs something that does not exist and fakes it, by
assuming it, bundling it as a hypothesis or using a weaker stand-in, `block`:
the real prerequisite comes first, as its own work. Say what it is, so that
an issue can be opened for it.

### Verdict

- `block` on any such fault. When blocking on doubt, name the statement, the
  suspected mismatch, and the check or source that failed to settle it.
- Approve only once you have tried to break every new statement and
  definition and failed.
