# Improving these instructions

**Looking for how to submit a tool?** That's [README.md](README.md) — this page
is about changing the instructions themselves.

Unclear instructions are bugs. If you got stuck, misread a requirement, or
followed a link that went nowhere, that is worth an issue even if you already
worked around it — you are the last person who will have fresh eyes on this.

## Report a problem

Open an issue here. Useful things to include: which page, what you expected,
and what you did instead. "I assumed a DOI was required before submitting" is a
perfect bug report.

## Propose a change

1. Fork, branch, edit.
2. Sign your commits — `git commit -s`. Same DCO rule that applies to tool
   submissions applies here.
3. Open a pull request describing what was unclear and how the change fixes it.

Prose changes, clarifications, typo fixes, and better examples are merged
readily. Two categories need more care:

- **Requirement text** (`docs/02-tiers.md`, the requirement IDs, tier
  boundaries, review SLAs, license policy) is **normative** — contributors and
  reviewers are held to it, and it is mirrored in the program's design record.
  Changes need the Editor-in-Chief's sign-off, not just a merge. Open an issue
  first and say what problem the current wording causes in practice.
- **Anything about PHI handling in Step 0** belongs upstream in
  [CreatingGithubRepoInstructions](https://github.com/brianmanderson/CreatingGithubRepoInstructions),
  not here. That repo is the single source of truth for scanning practice and
  its scanner rules; duplicating or forking that guidance here is how the two
  drift apart and start contradicting each other. Send scanner-rule fixes and
  detection-pattern improvements there; this repo should only ever describe
  how the Exchange's requirements *sit on top of* that guide.

## Style

Plain language, short sentences, and say the uncomfortable parts out loud —
what the badge does not certify, what a private repo does not protect you from,
what could go wrong. The audience is a working medical physicist who writes
code, not a software engineer, and who is skimming this between clinical tasks.

Prefer a concrete command or a filename over a description of one.
