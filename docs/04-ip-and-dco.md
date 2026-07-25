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
Signed-off-by: Your Name <your.email@example.com>
```

which `git commit -s` adds for you. It attests that you wrote the contribution,
or otherwise have the right to submit it under the stated open-source license.

### You do not need to sign your existing history

Most tools worth submitting were written long before you heard of this program,
and rewriting history to add trailers would break every clone, fork, and
citation pointing at your repo. So sign-off is **going-forward, not
retroactive** (R-11):

1. **Attest once, at submission.** Post this in your intake issue — it covers
   everything in the tree at the commit under review, and carries the same
   meaning as a trailer on each historical commit:

   ```
   I have the right to contribute the entire tree at commit <SHA> under
   <LICENSE>, and I submit it under the terms of the Developer Certificate
   of Origin (developercertificate.org).
   Signed-off-by: Your Name <your.email@example.com>
   ```

2. **Sign every commit from that day forward** with `git commit -s`. A bot
   enforces this on the frozen fork and it is expected on your live repo. If
   you start a new repo after joining, sign from the very first commit.

**You will not be returned for unsigned history.** You will be returned for
skipping the attestation, or for going back to unsigned commits afterward.

### The one rule about which address: it must be verified on your GitHub account

**Any domain is fine. Gmail, Yahoo, Hotmail, Proton, your university, your own
domain — we do not care, and a non-university address is never grounds for
returning a submission.** The DCO attests a real identity and your right to
contribute, not your affiliation.

What we do require: **the address you sign off with must be one you have added
and verified on your GitHub account.** That is what turns the trailer from a
line of text anyone could type into an attestation tied to a real, reachable
account.

There are good reasons to prefer a personal address, and none of them are our
business: you change jobs and the university address dies while the commits
live forever; your institution rewrites or blocks outbound mail; the work spans
two appointments; you keep your open-source identity separate from your
employer's mail system.

#### Adding and verifying the address (two minutes, one time)

1. GitHub → **Settings → Emails → Add email address**.
2. Click the confirmation link GitHub mails you. Unconfirmed addresses do not
   count — this is the whole point of the rule.
3. Set git to use that exact address (see below), and make sure it matches
   **character for character** — `J.Smith@gmail.com` and `j.smith@gmail.com`
   are the same mailbox to your mail provider but not necessarily the same
   string to a checker.

#### How to tell it worked

Open any of your commits on GitHub. If your **avatar and a clickable username**
appear next to it, GitHub has matched the commit email to your account and you
are fine. If you see a plain name with no avatar and no link, the address is
not on your account — fix that before you submit.

> **GitHub `noreply` addresses** (`12345+username@users.noreply.github.com`)
> are account-owned by construction and are fine to sign with if you prefer not
> to publish a real address. This is the right choice if privacy is what was
> pushing you toward an institutional address.

Two things this rule does **not** change:

- **Whether you have the right to release the code** — that is about who owned
  the work, not which mailbox you sign from. A verified Gmail on the commit
  does not make employer-owned code yours. Everything above this section still
  applies.
- **The Institution field on the intake form**, which stays required. It is
  used for reviewer-independence checks (we cannot assign you a reviewer from
  your own shop if we don't know your shop), not for identity verification.

### Signing off in practice

```bash
git config --global user.name  "Your Name"
git config --global user.email "your.email@example.com"   # must be verified on GitHub

git commit -s -m "Add dose-grid resampling"      # -s adds the trailer
```

GitHub Desktop does not add the trailer for you — type it as the last line of
the commit description, exactly matching your git `user.name` and `user.email`.

> **Pre-existing repositories with long histories: do nothing.** Settled by
> R-11 — historical commits never need signing. Post the submission-time
> attestation above and sign from that day forward. **Do not** run
> `git rebase --signoff` over shared history to "fix" it: rewriting published
> history breaks other people's clones and forks, and the rule does not ask
> for it. (`git rebase --signoff <base>` is only ever appropriate on a branch
> you have never shared.)

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
