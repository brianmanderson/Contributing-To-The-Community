# Contributing to the Medical Physics Community Code Exchange

**This repo is the front door.** It tells you how to get a tool from "a folder
on my machine" to a peer-reviewed, citable, badged entry in the Exchange index.

The Exchange is a curated, peer-reviewed index of open-source software for
radiation oncology and medical physics. **You keep your repository.** At
acceptance we mint a citation and a frozen, badged snapshot pinned to the exact
commit that was reviewed. Review is open and public, JOSS-style — your
reviewers are named, and so is their work.

> **Status: pilot — submissions are open.** The
> [index repo](https://github.com/medphys-code-exchange/index) is live, and it
> carries the intake form, the submission scanners, and the published index.
> Two things are still being wired, and it is only fair to say so up front:
> DOI minting is not yet connected, so a DOI for an early acceptance is
> back-filled into your `CITATION.cff` once it is; and the reviewer pool is
> still small, so turnaround can run past the 30-day target. Submitting now
> means being among the first tools indexed.

---

## The path, end to end

| Step | What you do | Where |
|---|---|---|
| **0** | Get your repo safe and public-ready: **no PHI, ever** | [docs/01-repo-hygiene.md](docs/01-repo-hygiene.md) → [CreatingGithubRepoInstructions](https://github.com/brianmanderson/CreatingGithubRepoInstructions) |
| **1** | Pick your tier and meet its requirements | [docs/02-tiers.md](docs/02-tiers.md) |
| **2** | License it, cite it, and confirm you have the right to release it | [docs/03-licensing.md](docs/03-licensing.md) · [docs/04-ip-and-dco.md](docs/04-ip-and-dco.md) |
| **3** | Run the pre-submission self-check until it's clean | [checklists/pre-submission.md](checklists/pre-submission.md) |
| **4** | Open a Tool Submission issue | [docs/05-submitting.md](docs/05-submitting.md) |
| **5** | Work the public review; get accepted | [docs/06-after-acceptance.md](docs/06-after-acceptance.md) |

---

## Step 0 comes first, and it is not ours

Before anything else: **your repository must contain no patient data.** Not in
the working tree, not in the git history, not in a private repo you plan to
make public later. Once PHI is committed it is in history forever unless the
history is rewritten; once it is pushed, it has left your institution.

That problem is already solved, carefully, in a separate public repo — and we
are not going to re-implement it:

> ### 👉 [github.com/brianmanderson/CreatingGithubRepoInstructions](https://github.com/brianmanderson/CreatingGithubRepoInstructions)
>
> Step-by-step: how to take existing work on your laptop and publish it to
> GitHub without letting PHI out. It ships a **PHI Scan desktop app**
> (double-click `.exe`, no Python, no terminal — [Releases](https://github.com/brianmanderson/CreatingGithubRepoInstructions/releases)),
> the identical scanner as a Python script, a pre-commit hook, a GitHub Action
> tripwire, a medical-project `.gitignore` template, and a guide to thinking
> about `.gitignore` rather than blindly copying one.
>
> Its one rule, which is also ours: **scan and ignore first, commit second,
> push last.**

Read that repo, run its scanner on your project folder, and fix what it finds
**before** you come back here. [docs/01-repo-hygiene.md](docs/01-repo-hygiene.md)
explains how it fits with the Exchange's own submission scanners, and the few
places where publishing to the Exchange asks for more than that guide does.

*(That guide was written for a UC San Diego team, so it names a local catalog
and a local incident process. The method and the tooling are
institution-agnostic — substitute your own institution's privacy-incident
process wherever it says to notify Brian or UCSD Health.)*

---

## What you get

- **A DOI and a citation** — Zenodo DOI minted at acceptance (Tier 2 and
  Tier C) and back-filled into your `CITATION.cff`, so your tool is citable
  the way a paper is.
- **A badge that means something** — it certifies a specific commit at a
  declared tier, with the platform versions it was verified against and the
  date. Not a participation trophy.
- **Visibility** — an index entry in front of the people who need your tool.
- **Your repo stays yours** — stars, issues, identity, and future development
  all stay on your repository. The org's frozen fork is an archive pinned to
  the reviewed commit, banner-linked back to you.
- **Reviewer credit** — reviewers are named publicly, and accepted
  contributors become eligible reviewers. That is how the pool scales.

## What we will not accept

- **Any PHI.** Not de-identified-by-eye, not "just the header." See Step 0.
- **Vendor binaries.** Never commit `VMS.TPS.*.dll` or any other vendor
  assembly. ESAPI and RayStation scripts are fully in scope — reference the
  assemblies from the local install and declare your tested platform versions.
- **Non-OSI licenses**, including "free for academic/non-commercial use."
- **A missing DCO attestation.** Your existing history does not need signing —
  post the submission-time attestation in your intake issue, then sign new
  commits with `git commit -s`.

---

## Contents of this repo

```
docs/01-repo-hygiene.md    PHI + git hygiene; how the scanners layer
docs/02-tiers.md           Tier 1 / Tier 2 / Tier C requirements (normative)
docs/03-licensing.md       License policy
docs/04-ip-and-dco.md      Who owns your code, and what sign-off means
docs/05-submitting.md      The intake form and what happens next
docs/06-after-acceptance.md  Frozen fork, DOI, badge, re-verification, promotion
docs/faq.md                Short answers to the recurring questions
checklists/pre-submission.md  Author self-check, by tier
```

The files you copy into your own repository — `README.template.md`,
`CITATION.cff.template`, `gitignore_esapi.template`, and the three CI
workflows — live in the index repo, at
[templates/](https://github.com/medphys-code-exchange/index/tree/main/templates).
They are kept there rather than here so there is exactly one copy: these pages
had already drifted from it once, and a stale copy of a scanner workflow is
worse than no copy at all.

## Questions, corrections, and improving this guide

Instructions that are wrong or unclear are a bug. Open an issue here — see
[CONTRIBUTING.md](CONTRIBUTING.md) for how to propose a change to these pages.

Maintainer: Brian M. Anderson, PhD, DABR — UC San Diego, Radiation Medicine &
Applied Sciences.
