{{/* The reviewer's four angles (review.md), in short, for authors to check before they push. */ -}}
- **Correct.** Each statement and definition says what it should: its
  quantifiers and edge cases (dimension zero, odd dimension, a degenerate
  form), the sign conventions of the atlas page it serves; no hypothesis
  that is the claim's content, no placeholder, no new predicate without a
  theorem that uses it or an example. A milestone has the atlas's
  hypotheses and conclusion, under the library's conventions, or
  `ERRATA.md` records the error as `AGENTS.md` says. Main theorems use only
  the standard axioms.
- **Not a duplicate.** You searched Mathlib, Tau Ceti and this library for
  each new declaration and for the steps of each long proof, including the
  declarations that the atlas page's correspondence list names, and the
  open pull requests. No thin wrapper restates what exists.
- **In scope.** It does what its issue asks and nothing unrelated, as one
  topic, as the design says, with the API its new definitions need. The
  description says what it does and why, names the sources it follows, and
  ends with its `Closes #…` line (`Part of #…` for a pull request that only
  adds an unresolved entry to `ERRATA.md`).
- **Credited, and no atlas text.** The module docstrings name the published
  sources the work follows. No prose copies the atlas's text: not in code,
  comments, the description or commit messages. A milestone's name, a Lean
  declaration's name, a formula and a citation of a published source are
  not copies. Write what you post in your own words from the start: a
  posted description is public at once. Run the atlas check below before
  you push or post, and reword each passage it finds that follows the
  atlas. Never quote what it prints, in a comment, a commit message or the
  description.
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

The atlas check searches `/atlas` for every run of eight words, ignoring
case and punctuation, in the files the branch changes, its commit messages
and the description. Save the description you will post as
`/tmp/description.md` (in a fix job, the pull request's current one, from
`gh pr view <number> --json body -q .body`, with your changes), and post
that file (`gh pr create --body-file /tmp/description.md`, or
`gh pr edit <number> --body-file /tmp/description.md`). Then run:

```
git log --format=%B origin/main..HEAD > /tmp/commits.txt
node - $(git diff --name-only --diff-filter=d origin/main...) /tmp/commits.txt /tmp/description.md <<'EOF'
const fs = require("fs"), path = require("path");
const words = t => t.toLowerCase().match(/[a-z]+/g) || [];
const walk = d => fs.readdirSync(d, { withFileTypes: true }).flatMap(e =>
  e.isDirectory() ? walk(path.join(d, e.name)) : [path.join(d, e.name)]);
const atlas = new Set();
for (const f of walk("/atlas").filter(f => /\.(md|bib|tex)$/.test(f))) {
  const w = words(fs.readFileSync(f, "utf8"));
  for (let i = 0; i + 8 <= w.length; i++) atlas.add(w.slice(i, i + 8).join(" "));
}
for (const p of process.argv.slice(2)) {
  const w = [], line = [];
  fs.readFileSync(p, "utf8").split("\n").forEach((l, n) =>
    words(l).forEach(x => { w.push(x); line.push(n + 1); }));
  for (let i = 0; i + 8 <= w.length; ) {
    let j = i;
    while (j + 8 <= w.length && atlas.has(w.slice(j, j + 8).join(" "))) j++;
    if (j > i) { console.log(`${p}:${line[i]}: ${w.slice(i, j + 7).join(" ")}`); i = j; }
    else i++;
  }
}
EOF
```

Each line it prints gives a file, the line where a run starts, and the run
of words that the atlas also has.
