{{/* Adapted from TauCetiReview's rubrics/scope.md and attribution.md (Apache-2.0); see README.md. */ -}}
## Angle 3: Scope, attribution and the private atlas

Three questions: does the pull request belong here now, as one unit; does it
credit what it drew on; and does it keep the atlas's text out of this public
repository? This angle may `block`.

### Scope

The plan is the tree of issues that grows from the root issue of each atlas
page, together with `DESIGN.md`, the parts' designs under `design/`, and
accepted follow-up issues. A pull request is in scope when it does what its
issue asks (`Closes #…`, or `Part of #…` for an errata-only pull request),
and that issue belongs to the plan.

- **New material serves the issue.** Every new definition, theorem or file is
  something the issue asks for, or a prerequisite it really needs: you can
  see the path from it to what the issue asks. "Might be useful later", or a
  long speculative chain, is not a prerequisite. But do not reject the
  infrastructure the issue needs: building what is missing is the point.
- **It fits the design.** The parts, files and names follow `DESIGN.md` and
  the part's design. A departure needs a reason, and a change to the design
  in the same pull request or an issue that proposes one.
- **Refactors are in scope** when their issue asks for one: reworking merged
  material needs no new claim on the plan. A refactor that its issue does not
  ask for, bundled with new work, is a second topic.
- **One topic.** Several unrelated pieces of work, or an opportunistic
  refactor bundled with new work, need a split. The file moves that
  placement requires next to a new file are part of the topic.
- **Size.** At most 2000 added lines, except a move of Tau Ceti, which is
  never split.

### Attribution

- Credit the sources the work follows: the book or paper, such as
  McDuff–Salamon, in the module docstring's references, with the atlas's
  `references.bib` as the guide to what to cite; and any formalization it
  copies or closely adapts, such as a Mathlib or Tau Ceti pull request.
- Watch for laundering: following an identifiable source's order of results,
  notation or proof plan is enough to need credit, even with no text copied.
- Do not ask for credit for routine work that follows nothing in particular.
  The atlas itself is not credited in files: a milestone's docstring line,
  "Milestone: *…*", is the only place a file mentions it.

### The private atlas

The atlas is private and this repository public, so nothing in the pull
request may copy the atlas's text: not the code, docstrings, comments, the
description, commit messages or an `ERRATA.md` entry. A milestone's name is
the only text of the atlas that may appear. Mathematics stated in Lean, and
explanations in the author's own words, are not copies. Compare distinctive
phrases of the pull request's prose with the atlas page under `/atlas` by
grep.

### Verdict

- `block` when new material does not serve its issue, the pull request is
  not one topic, or it copies the atlas's text; and when it closely follows
  identifiable existing work (a pull request, a paper, a formalization)
  without credit.
- `request changes` when the description does not say what it does and why,
  or lacks its `Closes #…` line; when it departs from the design without a
  reason; when it adds more than 2000 lines without being a move of Tau
  Ceti; or when a central source is named in the description but not in the
  code, or followed but not named.
- Approve when the pull request does its issue, as one unit, fits the design,
  credits its central sources, and keeps the atlas's text out.
