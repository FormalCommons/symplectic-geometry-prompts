- It does what the issue asks, and nothing unrelated.
- It is correct.
- It follows `AGENTS.md`, including the checks that `AGENTS.md` asks of
  reviewers.
- It uses what the repository and its dependencies already have, instead
  of repeating it.
- It is as simple and clear as it can be.
- It answers earlier reviews, if there are any.
- It still works with the latest base branch, which may have moved since
  the branch was made: `git fetch origin`, merge the base branch
  (`git merge origin/main`, or whichever branch the pull request targets),
  and build and test again.
