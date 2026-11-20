# Symplectic geometry prompts

The prompts that [fc-worker](https://github.com/FormalCommons/fc-worker)
gives the agents that build
[symplectic-geometry](https://github.com/FormalCommons/symplectic-geometry).
The workers follow this repository's `main` branch during a run: a change
merged here reaches every job that starts a minute or so later, with no
restart.

| File | Job |
|---|---|
| `work.md` | An issue that is ready: do it, split it, or propose closing it. |
| `fix.md` | A pull request that needs a fix. |
| `review.md` | A pull request that needs a review. |
| `triage.md` | An issue labelled `proposed` or `close-proposed`. |
| `_checks.md` | The points that work, fix and review jobs check, which they include. |

Each prompt is a Go [text/template](https://pkg.go.dev/text/template), with
the fields that fc-worker's README lists, such as `{{.Repo}}` and
`{{.Number}}`. A file named `_*.md` is included with
`{{template "_name.md" .}}`. The prompts started as fc-worker's example
prompts at
[`cc836b4dfea2`](https://github.com/FormalCommons/fc-worker/tree/cc836b4dfea2e20fd4a8ac8ea1a42959bafca3b4/prompts).

## Changing a prompt

Open a pull request; `main` takes no direct pushes. Every round comment
that fc-worker writes says which commit of this repository the job's
prompt came from ("with prompts at …"), so the effect of a change can be
followed through the run. The agents cannot push here: their tokens cover
only the library's repository.

## Licence

[Apache 2.0](LICENSE).
