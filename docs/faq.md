# FAQ

**Isn't this just GitHub with extra steps?**
GitHub solved hosting. It did not solve *finding* the right tool, *trusting*
it, or *citing* it. The Exchange is curation, review, and a citable record —
the parts that make a physicist willing to build on someone else's code
instead of rewriting it for the fourth time.

**Do I have to move my repository into your organization?**
No. You keep your repo — stars, issues, identity, and all future development.
The org creates a frozen fork pinned to the reviewed commit, purely as an
archival guarantee, with a banner pointing back at you.

**Do I need a DOI before submitting?**
No. It's minted at acceptance (Tier 2 and Tier C) and back-filled into your
`CITATION.cff` by a pull request you merge. Tier 1 gets an index entry and
badge, no DOI.

**Which DOI ends up in my `CITATION.cff` — the versioned one?**
No, the concept DOI, which always resolves to your newest release. That way
the line stays correct every time you publish and you never have to update it.
The index entry records the version DOI for the reviewed release, since the
badge certifies that specific commit. If your repo has a `.zenodo.json`, note
that Zenodo ignores `CITATION.cff` completely in its favour — see
[06-after-acceptance.md](06-after-acceptance.md).

**My code is an ESAPI script. Is that in scope?**
Yes, fully — vendor-API code is a large share of what physicists actually
re-implement. What you must never do is commit vendor assemblies (`VMS.*.dll`
and friends); reference them from the local install and declare your tested
Eclipse/ESAPI versions. See [01-repo-hygiene.md](01-repo-hygiene.md#vendor-binaries-never-committed-no-exceptions).

**RayStation?**
Also in scope, but whether RaySearch's terms permit redistribution of certain
script patterns is an open question the program has not yet resolved. Submit
and flag it as RayStation; your review will be queued behind that answer.

**What if my tool is a thin wrapper / only 200 lines?**
Submit it. Size is not a criterion; usefulness and reproducibility are. Plenty
of the most-rewritten code in the field is small.

**Which tier should I pick?**
If the output could plausibly inform a clinical decision — plan checks, dose
calculations, QA analysis, structure evaluation, transfer checks — it is
**Tier C**, and asking for Tier 1 to duck the bar just costs a cycle. Otherwise
Tier 2 if you have tests, docs, and a tagged release; Tier 1 if you don't yet.
Tier 1 → Tier 2 promotion is supported.

**Can I sign off with a personal email instead of my university address?**
Yes — any domain is fine (Gmail, Yahoo, Hotmail, your own), and a
non-university address is never grounds for returning a submission. The one
requirement is that the address be **added and verified on your GitHub
account**; unconfirmed addresses don't count. Quick check: open one of your
commits on GitHub — if your avatar and a clickable username appear, you're
set. See [04-ip-and-dco.md](04-ip-and-dco.md#the-one-rule-about-which-address-it-must-be-verified-on-your-github-account).
(Separately: the intake form's Institution field stays required, because
reviewer-independence checks depend on knowing where you work.)

**My repo has years of unsigned commits. Do I have to rewrite history?**
No — settled policy (R-11). Historical commits never need signing, and you
should **not** rewrite published history to add trailers (it breaks everyone
else's clones and forks). Post the submission-time attestation in your intake
issue — one statement covering the whole tree at the reviewed commit — then
sign every commit from that day forward with `git commit -s`. See
[04-ip-and-dco.md](04-ip-and-dco.md#you-do-not-need-to-sign-your-existing-history).

**Is a private repo enough while I get organized?**
Private is the right default while you're still finding out what's in your
folder, and it's what [CreatingGithubRepoInstructions](https://github.com/brianmanderson/CreatingGithubRepoInstructions)
recommends. But **private is not HIPAA-compliant** — PHI in a private repo is
still a reportable incident. And Exchange submissions must end up public, so
the scan has to be genuinely clean either way.

**The scanner flagged a test fixture with fake MRNs. Now what?**
Say so in your review thread; a reviewer can clear a documented false positive,
and the rules improve. Do not silently disable the check.

**What if the scanner returns exit code 2?**
That's an environment error (usually `pydicom` missing), not a pass. Fix it
and re-run — the scanners fail closed on purpose.

**How long does review take?**
Target is 30 days submission → decision, with reviewers capped at 2–3
concurrent reviews. The program tracks and publishes actual turnaround.

**What happens if I stop maintaining the tool?**
Your entry flips to "Archived — verified as of [date], unverified since" after
24 months without renewal. Nothing is deleted; the DOI stays resolvable. A
stale-but-labeled tool is more useful than a deleted one.

**Can I review other people's submissions?**
Yes, once you've had a submission accepted — that's the intended path. Review
is named, public, citable professional service.

**Who runs this?**
Brian M. Anderson, PhD, DABR (UC San Diego) as Editor-in-Chief, with a co-lead
being recruited. The long-term goal is an AAPM working group; the pilot is
running in parallel because AAPM timelines are measured in years.

**Something here is wrong or unclear.**
That's a bug — open an issue in this repo. See [CONTRIBUTING.md](../CONTRIBUTING.md).
