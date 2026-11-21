{{/* Adapted from TauCetiReview's rubrics/scope.md and attribution.md (Apache-2.0); see README.md. */ -}}
## Angle 3: Scope, attribution and the private atlas

Three questions: does the pull request do its issue, as one unit; does it
credit what it drew on; and does it keep the atlas's text out of this public
repository? This angle may `block`.

### Scope

The atlas is the plan, as `AGENTS.md` says. The work toward it is a tree of
issues, one root issue per atlas page, together with `DESIGN.md` and the
parts' designs under `design/`. A pull request does its issue: its
description ends with `Closes #…`, or with `Part of #…` if it only adds an
unresolved entry to `ERRATA.md`. An open issue without the `proposed` label
has been accepted; do not judge whether it should exist. If you doubt that
it should, say so in your summary as work for an issue of its own. A pull
request that a person in the project opened needs no issue, and may change
the setup files.

- **New material serves the issue.** Every new definition, theorem or file is
  something the issue asks for, or a prerequisite it needs. The API that
  characterizes a new definition, as `AGENTS.md` and the design ask, and its
  statements at their natural generality, serve the issue too: the library
  is meant to be used. "Might be useful later", or a long speculative chain,
  is not a prerequisite.
- **It fits the design.** The parts, files and names follow `DESIGN.md` and
  the part's design. A departure needs a reason in the description, and a
  change to the design in the same pull request or an issue that proposes
  one.
- **Refactors are in scope** when their issue asks for one: reworking merged
  material needs no new claim. A refactor that its issue does not ask for,
  bundled with new work, is a second topic.
- **One topic.** Several unrelated pieces of work, or an opportunistic
  refactor bundled with new work, need a split. Material that does not
  belong is removed from the pull request and becomes an issue of its own.
  The file moves that placement requires next to a new file are part of the
  topic.
- **Size.** At most 2000 added lines, and at most 1000 lines in a new file,
  except a move of Tau Ceti, which is never split.
- **Setup files.** A change to `lakefile.toml`, `lake-manifest.json` or
  `lean-toolchain` belongs to a move of Tau Ceti ("Move Tau Ceti to …",
  opened by `github-actions[bot]`) or to an issue a person in the project
  opened. CI checks how a move changes them, not who may.
- **Designs.** For a pull request that adds or changes `DESIGN.md`, check
  that every milestone of the page has a part, and that the parts can be
  built in the order given from what exists. For a part's design, check that
  it fits the overview, states its milestones as the atlas, or `ERRATA.md`,
  does, and lists the issues to split its part into.
  If it changes which parts or issues build on which, so that an open
  issue needs a blocker added or removed, check that an open issue asks
  for each such change and waits for this pull request's issue, if it has
  one.

### Attribution

- Credit the sources the work follows: the book or paper, such as
  McDuff–Salamon, in the module docstring's references, with the atlas's
  `references.bib` as the guide to what to cite; and any formalization it
  copies or closely adapts, such as a Mathlib or Tau Ceti pull request.
- Watch for laundering: following an identifiable source's order of results,
  notation or proof plan is enough to need credit, even with no text copied.
- Do not rely on the description to name what was adapted. Where the design
  or a docstring names a Tau Ceti or Mathlib counterpart of a new definition
  or main theorem, or the reuse search finds one, open it and compare the
  proofs: the same construction and the same steps in another setting need
  credit in the module docstring, by the name of the declaration adapted.
- Do not ask for credit for routine work that follows nothing in particular.
  The atlas itself is not credited in Lean files: a milestone's docstring
  line, "Milestone: *…*", is the only place a Lean file mentions it.

### The private atlas

The atlas is private and this repository public, so nothing the pull request
adds may copy the atlas's text: not the code, docstrings, comments, the
description or an `ERRATA.md` entry. Mathematics stated in Lean,
explanations in the author's own words, a milestone's name, a Lean
declaration's name, a formula and a citation of a published source are not
copies. To check, take runs of about eight consecutive words from the pull
request's prose, in plain words with formulas left out, and search all of
`/atlas` for them (`grep -rF`); read closely any passage that follows the
atlas sentence by sentence. Report a copy by file and line on both sides,
without quoting it. Commit messages cannot be changed without rewriting
history, and the merge uses the pull request's title and description, so a
copy there is a note for the maintainer in your summary, not a finding.

### Verdict

- `block` when the pull request as a whole does not do its issue, or closely
  follows identifiable existing work (a pull request, a paper, a
  formalization) without credit.
- `request changes` for material that does not belong to the issue or a
  second topic (remove it, and open an issue for it); a copy of the atlas's
  text in a file or the description; a description that does not say what
  it does and why, names no sources, or lacks its `Closes #…` or
  `Part of #…` line; a departure from the design without a reason; a size
  limit exceeded; a setup change outside a move or a person's issue; a
  design that misses a milestone or cannot be built in its order; a change
  to the build order with no issue to bring the blockers in line; or a
  central source named in the description but not in the code, or followed
  but not named.
- Approve when the pull request does its issue, as one unit, fits the
  design, credits its central sources, and keeps the atlas's text out.
