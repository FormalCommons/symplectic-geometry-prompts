# Symplectic geometry prompts

The prompts that [fc-worker](https://github.com/FormalCommons/fc-worker)
gives the agents that build
[symplectic-geometry](https://github.com/FormalCommons/symplectic-geometry).
The workers follow this repository's `main` branch during a run: a change
merged here reaches every job that starts a minute or so later, with no
restart.

| File | Job |
|---|---|
| `work.md` | An issue that is ready: do it, split it, change the blockers it names, or propose closing it. |
| `fix.md` | A pull request that needs a fix. |
| `review.md` | A pull request that needs a review. |
| `triage.md` | An issue labelled `proposed` or `close-proposed`. |
| `_checks.md` | The reviewer's angles in short, which work and fix jobs check before they push. |
| `_review-protocol.md` | The protocol every reviewer follows: untrusted input, an adversarial author, what to report. |
| `_angle-*.md` | The review's four angles, each judged by its own subagent: correctness, reuse, scope and attribution, library quality. |

Each prompt is a Go [text/template](https://pkg.go.dev/text/template), with
the fields that fc-worker's README lists, such as `{{.Repo}}` and
`{{.Number}}`. A file named `_*.md` is included with
`{{template "_name.md" .}}`. The prompts started as fc-worker's example
prompts at
[`cc836b4dfea2`](https://github.com/FormalCommons/fc-worker/tree/cc836b4dfea2e20fd4a8ac8ea1a42959bafca3b4/prompts).

## Reviews

A review job builds the pull request, then has four subagents judge it at
once, each from one angle: correctness and faithfulness; reuse and
duplication; scope, attribution and the private atlas; library quality.
It checks their findings and posts one review. The protocol and the angles
are adapted from the rubrics of
[TauCetiReview](https://github.com/TauCetiProject/TauCetiReview/tree/60472b7/rubrics)
(Apache 2.0) for a library built from the atlas: the plan is the atlas page,
`DESIGN.md` and the issues instead of Tau Ceti's roadmaps, reuse searches
Tau Ceti as well as Mathlib, and the atlas's text must stay out of the
public repository. A blocking finding becomes a request for changes; when a
prerequisite must come first, the reviewer opens an issue for it, and the
fix job marks it as the issue's blocker and closes the pull request, so that
a new work job takes the issue up once the prerequisite is done.

A design, a pull request that changes only the design, is reviewed for what
later steps could not put right: the milestones, the build order, the
mathematics, reuse of what exists, and fit with the merged design.
Choices that a part's design file or a building issue can still make are
notes for later steps, not requests for changes: the approving review
comments them on the open issue they concern, or the split along the
design carries them into the issues it creates, and fix jobs leave them
alone. In the first run, the overview design took seven rounds, and each
part design took three to seven.

## Changing a prompt

Open a pull request; `main` takes no direct pushes. Every round comment
that fc-worker writes says which commit of this repository the job's
prompt came from ("with prompts at …"), so the effect of a change can be
followed through the run. The agents cannot push here: their tokens cover
only the library's repository.

## Licence

[Apache 2.0](LICENSE).
