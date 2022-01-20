---
description: Eduardo/Daniel comments on handling PRs
---

# Notes on PRs

One of the current issues is that PRs take way too long to be merged, even though there is a strong bias towards accepting and merging a PR.

Here are a few hints and tips to handle PRs better:

1. A PR addresses a single issue and not several at the same time. If you are working on a feature PR, do not try to merge changes to unrelated documentation or unrelated tests.
2. It's okay to have PRs dedicated to enhancing documentation, testing, style, etc.
3. If ocamlformat says the format in your PR is bad, then it's bad and fix it.
4. Your PR should be explicit on the subjects of caveats and how main consequences are taken care of (example: explain how your work does not have an effect on recovery if it's not obvious it doesn't have one, convince everyone you are not breaking things).
5. A feature PR should be as small as possible: is your PR the smallest possible change to solve this problem?
6. Don't be the person who delays a PR: if you feel a comment/semi colon is missing, commit and submit, it'll speed up things.
