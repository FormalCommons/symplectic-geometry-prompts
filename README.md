# Symplectic geometry prompts

The prompts that [fc-worker](https://github.com/FormalCommons/fc-worker)
gives the agents that build
[symplectic-geometry](https://github.com/FormalCommons/symplectic-geometry).
The workers follow this repository's `main` branch during a run: a change
merged here reaches every job that starts a minute or so later, with no
restart.

| File | Job |
|---|---|
| `work.md` | An issue that is ready: do it, split it, change the blockers or texts of the issues it names, or propose closing it. Work that is too long for one job and must be one pull request is handed over as a draft. |
| `continue.md` | A draft pull request of the agents: work that a job could not finish in its time. Go on with it, and mark it ready when it is finished. |
| `fix.md` | A pull request that needs a fix. |
| `review.md` | A pull request that needs a review. |
| `triage.md` | An issue labelled `proposed` or `close-proposed`. |
| `_checks.md` | The reviewer's angles in short, with checks for what first reviews most often find, which work and fix jobs go through before they push. |
| `_review-protocol.md` | The protocol every reviewer follows: untrusted input, an adversarial author, what to report. |
| `_angle-*.md` | The review's four angles, each judged by its own subagent: correctness, reuse, scope and attribution, library quality. |

Each prompt is a Go [text/template](https://pkg.go.dev/text/template), with
the fields that fc-worker's README lists, such as `{{.Repo}}` and
`{{.Number}}`. A file named `_*.md` is included with
`{{template "_name.md" .}}`. `review.md` and `fix.md` use `{{.Leads}}`
and `{{.First}}`, which say that a pull request
[merges first](https://github.com/FormalCommons/fc-worker#merging-one-pull-request-first);
an fc-worker without these fields does not take up the prompts and keeps
the commit it had. The prompts started as fc-worker's example
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

When the author has only merged the base branch since an approval, as a
fix for a conflict does, the review job does not start the four subagents
again: it checks how each merge resolved its conflicts and that the merged
code builds. What the base branch brought in that the pull request could
now use becomes an issue and not a request for changes.

A pull request that merges first, such as a move to a new version of Tau
Ceti, holds the others out of the merge queue only from its first
approval. Before that, its review leaves out the check against the latest
base branch, which moves faster than a fix could follow, and its fix jobs
merge the base branch before they push. After the approval a fix job
merges the base branch once more and repairs what breaks, and the review
that follows covers only what changed since the approval.

A design, a pull request that changes only the design, is reviewed for what
later steps could not put right: the milestones, the build order, the
mathematics, reuse of what exists, and fit with the merged design.
Choices that a part's design file or a building issue can still make are
notes for later steps, not requests for changes: the approving review
comments them on the open issue they concern, or the split along the
design carries them into the issues it creates, and fix jobs leave them
alone. In the first run, the overview design took seven rounds, and each
part design took three to seven.

## Work that takes several jobs

A job has a fixed time, which its prompt gives as `{{.Deadline}}`, and
nothing but what it pushed outlives it. Work that must be one pull request
and takes longer, such as a move to a new version of Tau Ceti, goes
through a draft: the work job pushes as it goes and opens the pull request
as a draft whose description has a `## Progress` section, saying what is
done, what remains and what the next agent should know. fc-worker gives a
draft of the agents a continue job, again and again, until one finishes
the work, writes the description anew and marks the pull request ready.
Reviews, fixes and the merge queue start only then. A draft whose jobs
stop making progress waits for a person instead: after three jobs in a
row that end without a new commit, or after 20 rounds. In the first run,
before there was a continue job, the first move of the Tau Ceti pin ran
out of its 90 minutes with the library nearly repaired and nothing pushed,
and the next job began again from nothing.

## Changing a prompt

Open a pull request; `main` takes no direct pushes. Every round comment
that fc-worker writes says which commit of this repository the job's
prompt came from ("with prompts at …"), so the effect of a change can be
followed through the run. The agents cannot push here: their tokens cover
only the library's repository.

## Licence

[Apache 2.0](LICENSE).
