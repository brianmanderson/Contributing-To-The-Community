# Step 5 — After acceptance

Acceptance is a set of concrete, mechanical things. Here is all of them.

## What the org does

1. **Records the reviewed commit** — SHA, tier, platform matrix, review issue
   link, and date go into your metadata record. Everything downstream keys off
   that SHA.
2. **Cuts a frozen fork** — an org-owned fork named `frozen-<tool>`, pinned to
   the reviewed commit, carrying a banner README that points at *your* live
   repository. This is the archival copy: it guarantees the reviewed code
   remains retrievable at that exact state even if your repo moves, is renamed,
   or goes away.
3. **Mints a DOI** (Tier 2 and Tier C) — the frozen fork is tagged at the
   reviewed commit, Zenodo mints a DOI from that org-owned release, and the DOI
   is back-filled into your `CITATION.cff` by pull request **which you merge**.
   Nothing is pushed into your repository without your approval.
4. **Publishes your index entry and badge** — with your license, tier,
   platform matrix, verification date, and links to both the live repo and the
   frozen fork.
5. **Names your reviewers** on the entry, publicly and permanently.

## What stays yours

Everything that matters for your career. Stars, forks, issues, discussions,
contributor graph, and all future development stay on **your** repository. The
frozen fork does not compete with it — it carries a banner telling readers to
go to you for the live code.

The Exchange deliberately does not take custody of your project. The index is a
pointer with a certificate attached, not a landing zone.

## Your badge, and what it claims

> **Verified [date] — tested against [platform versions]**

It certifies **one commit** at **one tier** against **one declared platform
matrix**. It does not certify `main`, it does not certify your next release,
and — for Tier C — **it is not a clinical clearance**. The framing throughout
is "reference implementation requiring local commissioning."

Keep saying that out loud in your own README. Users who understand what the
badge means are users who won't misuse your tool.

## Staying verified

Verification lapses after **24 months**. When it does, your entry flips
automatically to:

> **Archived — verified as of [date], unverified since**

Nothing is deleted, ever. The entry stays up, the frozen fork stays up, the DOI
stays resolvable. The status change is disclosure, not punishment: an unmaintained
tool from three years ago is still the best starting point somebody has, as
long as they can see that's what they're picking up.

Renewing is cheap — either:

- the scans and CI are re-run on the frozen fork and pass, or
- you re-attest with an updated platform matrix (e.g. "also tested against
  ESAPI 19.0").

You'll be pinged before the deadline. Renewing takes minutes; letting it lapse
costs you nothing except an honest label.

## Promoting Tier 1 → Tier 2

A supported, expected path. Add the tests, docs, tagged release, and platform
matrix; request a re-review against the Tier 2 requirements. On success your
badge and entry update and a **new frozen fork** is cut at the newly reviewed
commit. The old one stays — the record of what was certified when is never
rewritten.

Submitting at Tier 1 first is a legitimate strategy: get indexed and visible,
then earn the higher bar.

## You are now eligible to review

Accepted contributors become eligible reviewers. This is the whole scaling
model — a curated index cannot outrun its reviewer pool, and everyone who has
been through the process knows exactly what it asks for.

Reviewing is real, documented, citable professional service: you are named on
every entry you review, with a link. The workload cap is 2–3 concurrent
reviews, and the target is 30 days each. If you want in, say so in your review
thread or open an issue in the [`index`](https://github.com/medphys-code-exchange/index)
repo.

## Changing or withdrawing an entry

- **New version of your tool?** Nothing breaks. Your badge continues to certify
  the reviewed commit; submit a re-review when you want the badge to move
  forward. Your live repo can move as fast as you like.
- **Want to correct entry metadata?** Open an issue in the `index` repo.
- **Want out?** Say so and the entry is marked withdrawn. The frozen fork and
  DOI remain — a minted DOI is a permanent scholarly record and cannot be
  retracted quietly. That permanence is the point of having one.
