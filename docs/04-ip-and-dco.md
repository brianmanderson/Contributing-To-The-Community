# Step 2b — Before you attest: does your employer own your code?

If you wrote your tool as part of your job — on work time, on work equipment,
or within your scope of employment — **your institution very likely owns it.**
This is true at nearly every university and hospital system (University of
California policy, for example, assigns such rights to UC).

Signing off on a submission (the DCO, below) is a legal attestation that you
have the right to contribute the code. **Attesting without checking is the most
common honest mistake in open source**, and it is the one that can actually
cause you a problem later.

## The good news

Institutions almost always say yes. Open-source release costs them nothing,
generates cited output, and tech-transfer offices have a routine process for
it. The 15 minutes below is nearly always 15 minutes of paperwork, not a
negotiation.

Be honest about what you are asking for. An OSI-approved license **cannot be
restricted to non-commercial use** — Apache-2.0 explicitly grants commercial
rights. If you request approval for something narrower than the license
actually conveys, the sign-off you get back does not cover the release you are
making.

## What to do (15 minutes)

1. Find your institution's technology transfer / innovation office.
2. Send this email:

   > **Subject:** Open-source release approval — [tool name]
   >
   > I've developed a software tool ([one-sentence description]) in the course
   > of my work and would like to release it under an OSI-approved open-source
   > license ([Apache-2.0]), which permits reuse including commercial reuse —
   > that is what open-source release means. The release is for submission to a
   > peer-reviewed medical physics code index. Could you confirm approval or
   > point me to the required process?

3. **Keep the reply.** You do not send it to us — the DCO is your attestation,
   not a form we process — but you want it in your own records.

## What signing off actually is

The **Developer Certificate of Origin (DCO)**: a line on each commit reading

```
Signed-off-by: Your Name <you@institution.edu>
```

which `git commit -s` adds for you. It attests that you wrote the contribution,
or otherwise have the right to submit it under the stated open-source license.

A bot checks that every commit in the submitted range carries the line.
**Submissions with unsigned commits are returned before review starts** — this
is automated and impersonal, so save yourself the round trip.

### Signing off in practice

```bash
git config --global user.name  "Your Name"
git config --global user.email "you@institution.edu"

git commit -s -m "Add dose-grid resampling"      # -s adds the trailer
```

To sign off commits you already made, on a branch you have not shared:

```bash
git rebase --signoff <base-commit>               # adds the trailer to a range
```

GitHub Desktop does not add the trailer for you — type it as the last line of
the commit description, exactly matching your git `user.name` and `user.email`.

> **Pre-existing repositories with long histories:** whether the DCO
> requirement applies to *every historical commit* or only to the submitted
> range is a policy point the program is still finalizing. If your repo has
> years of unsigned history, **submit anyway and say so in the intake issue** —
> do not rewrite years of history on your own initiative. Rewriting history to
> satisfy a rule that may not require it is the worse outcome.

## Special cases

- **Vendor research agreements** (Varian, RaySearch, and similar): code that
  exposes non-public API behavior learned under such an agreement **cannot be
  submitted**, regardless of your institution's approval. This is the one case
  where a tech-transfer yes isn't enough.
- **Grant-funded code:** federal funding generally *encourages* open release,
  but check your award terms for software- and data-sharing clauses.
- **Prior-employer code:** work you wrote at a previous job belongs to that
  employer. A from-scratch rewrite is yours (or your current employer's).
- **Multiple authors:** every commit author needs their own sign-off. Get it
  before you submit, not during review.
