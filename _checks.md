{{/* The reviewer's four angles (review.md), in short, for authors to check before they push. */ -}}
- **Correct.** Each statement and definition says what it should: its
  quantifiers and edge cases (dimension zero, odd dimension, a degenerate
  form), the sign conventions of the atlas page it serves; no hypothesis
  that is the claim's content, no placeholder, no new predicate without a
  theorem that uses it or an example. A milestone has the atlas's
  hypotheses and conclusion, or `ERRATA.md` has its entry with a
  counterexample. Main theorems use only the standard axioms.
- **Not a duplicate.** You searched Mathlib, Tau Ceti and this library for
  each new declaration and for the steps of each long proof, including the
  declarations that the atlas page's correspondence list names, and the
  open pull requests. No thin wrapper restates what exists.
- **In scope.** It does what its issue asks and nothing unrelated, as one
  topic, as the design says. The description says what it does and why,
  names the sources it follows, and ends with its `Closes #…` line.
- **Credited, and no atlas text.** The module docstrings name the published
  sources the work follows. Nothing copies the atlas's text, in code,
  comments, the description or commit messages; a milestone's name is the
  only text of it that may appear.
- **Good library code.** A minimal public surface with the API that
  characterizes each definition (`foo_def`, `mem_foo_iff`, `@[ext]`,
  `@[simp]`); statements at their natural generality and in their natural
  files, as `AGENTS.md` and `DESIGN.md` say; Mathlib-style names in the
  right namespace; docstrings about the mathematics; robust proofs, with
  long ones split into lemmas.
- **It answers earlier reviews**, if there are any.
- **It still works with the latest base branch**, which may have moved since
  the branch was made: `git fetch origin`, merge the base branch
  (`git merge origin/main`, or whichever branch the pull request targets),
  and build and test again.
