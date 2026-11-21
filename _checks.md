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
  open pull requests. No thin wrapper restates what exists. Search again
  on that diff, Tau Ceti as hard as Mathlib, since most duplicates that
  reviews find are steps proved inline: for each new lemma, `private` ones
  included, and each `have` that takes more than a few lines and would
  hold outside its proof, grep the three source trees for the identifiers
  of its statement. Grep is the main search: most of what reviews find is
  a known lemma, specialized or unfolded. Then state those you still doubt
  as `example`s closed by `exact?`, in one scratch file under `/tmp` that
  imports `Mathlib` and your file, and run it once
  (`lake env lean /tmp/….lean`). `exact?` sees only what the scratch file
  imports.
- **In scope.** It does what its issue asks and nothing unrelated, as one
  topic, as the design says, with the API its new definitions need. The
  description says what it does and why, names the sources it follows, and
  ends with its `Closes #…` line (`Part of #…` for a pull request that only
  adds an unresolved entry to `ERRATA.md`). The description claims only
  what the diff does: each declaration it names is there, and is used
  where it says. If the issue says how to tell that it is done, that test
  passes on the branch merged with the base branch.
- **The design matches.** Where the pull request adds or moves a file,
  imports a file of another part, or gives a name, a statement or an
  attribute that differs from the design's, the design says so as the pull
  request leaves it. Record it in this pull request: in the part's design
  file, or in the part's section of `DESIGN.md` if it has no file. A file
  you add, or an import of another part's file, goes in that one file
  only: grep it for a neighbouring file's name to find the places. Where
  the part has a design file, do not add it to `DESIGN.md`, whose lists of
  a part's files and of what a part uses need not be complete: every
  part's pull requests change `DESIGN.md`, and a conflict there costs a
  fix and a second review. If such an addition of yours conflicts in
  `DESIGN.md`, keep the base branch's lines and drop yours. A moved file,
  or a changed name, statement or attribute, is corrected wherever
  `DESIGN.md` or `design/` gives the old one: grep for it. Change only the
  lines that name what changed, write no more than the code shows, and
  give the reason in the description. A lemma you add
  beyond those the design names needs no entry: do not add it to the
  design's file table or to its list of that file's declarations. Other
  open pull requests change those lines, and a conflict there costs a fix
  and a second review. If it makes a sentence of the design false, such as
  a count, correct that sentence only. Where the design is wrong in more
  than that, such as a definition, a milestone or the build order, do as
  `AGENTS.md` says: propose the change in an issue.
- **Blockers that match the design.** Agents do not change other issues'
  blockers, so they stay as they were set. If the work changes which parts
  or issues build on which (the build order in `DESIGN.md`, a part's
  *Builds on*, the order of a design file's issues), so that an open issue
  needs a blocker added or removed, then once the pull request is open,
  create an issue, labelled `proposed`, that names the pull request and
  each such change, unless an open issue already asks for it. Mark it as
  blocked by the issue the pull request closes as soon as you create it,
  so that it waits for the merge.
- **Credited, and no atlas text.** The module docstrings name the published
  sources the work follows. A proof that adapts one from Tau Ceti or
  Mathlib, with the same steps in another setting, is credited in the
  module docstring by the name of the declaration it adapts; the
  description alone is not enough. No prose copies the atlas's text: not
  in code, comments, the description or commit messages. A milestone's
  name, a Lean declaration's name, a formula and a citation of a published
  source are not copies. Write what you post in your own words from the
  start: a posted description is public at once. Run the atlas check
  below before you push or post, and reword each passage it finds that
  follows the atlas. Never quote what it prints, in a comment, a commit
  message or the description.
- **Good library code.** A minimal public surface with the API that
  characterizes each definition (`foo_def`, `mem_foo_iff`, `@[ext]`,
  `@[simp]`); statements at their natural generality and in their natural
  files, as `AGENTS.md` and `DESIGN.md` say; Mathlib-style names in the
  right namespace; docstrings about the mathematics; robust proofs, with
  long ones split into lemmas. Reviews most often find the following, so
  check each on that diff:
  - a `private` lemma that is not a step of one proof. One whose statement
    mentions only Mathlib or Tau Ceti types and whose proof uses nothing
    of this file's subject, or one that several proofs use, is public, in
    the file and namespace of its subject, with a Mathlib-style name and
    at its natural generality;
  - a docstring that says more than its statement, or the reverse of it.
    Read each docstring you wrote, or whose declaration you changed,
    against the statement: the direction of a map or an implication, the
    hypotheses, and each thing it says the conclusion gives;
  - `@[simp]` on a lemma that `simp` already proves, or whose left side
    `simp` rewrites. In a scratch file under `/tmp` that imports the files
    you changed, `#lint only simpNF in SymplecticGeometry` reports none of
    your lemmas;
  - inside a proof, a `rfl`, `change`, `show`, or a closing `exact` or
    `rwa`, that works only by unfolding a definition through a wrapper or
    a coercion. Use the lemma that states the equality, or add it (its own
    proof may be `rfl`); a `change` or `show` that stays has a comment
    saying why it is needed;
  - an import that the file does not use, and a step proved twice in one
    file;
  - a definition without the lemmas that say how it meets the operations
    around it, and a lemma not named after its statement as its neighbours
    are.
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
of words that the atlas also has. A commit already pushed cannot be
reworded without force-pushing: leave it, and say in your comment that its
message needs a maintainer, without quoting it. Check an issue or comment
you create the same way, by saving its text to a file and passing it too.
