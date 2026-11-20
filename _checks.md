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
  sources the work follows. Nothing copies the atlas's text, in code,
  comments, the description or commit messages; a milestone's name is the
  only text of it that may appear. Write what you post in your own words
  from the start: a posted description is public at once. Before you push
  or post, check it as the reviewer will, by searching `/atlas` for every
  run of eight words in the files you add or change and in the
  description, saved to a file under `/tmp`:

  ```
  python3 - <files> /tmp/description.md <<'EOF'
  import re, sys, glob
  words = lambda t: re.findall(r"[a-z]+", t.lower())
  atlas = set()
  for f in glob.glob("/atlas/**/*.md", recursive=True):
      a = words(open(f).read())
      atlas.update(" ".join(a[i:i+8]) for i in range(len(a) - 7))
  for p in sys.argv[1:]:
      w = words(open(p).read())
      hit = [" ".join(w[i:i+8]) in atlas for i in range(len(w) - 7)]
      i = 0
      while i < len(hit):
          j = i
          while j < len(hit) and hit[j]:
              j += 1
          if j > i:
              print(p, "|", " ".join(w[i:j+7]))
          i = max(j, i + 1)
  EOF
  ```

  Reword every match, except a milestone's name, a Lean declaration's
  name and a formula.
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
