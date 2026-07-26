# Steps 3–4 — Self-check, then submit

## Run the scanners yourself first

Do not make the CI find things you could have found. From the root of your
repository:

```bash
python phi_scan.py .
python vendor_binary_scan.py .
```

Both live in the Exchange's [`index`](https://github.com/medphys-code-exchange/index)
repo under `scripts/`. `phi_scan.py` needs `pydicom` (`pip install pydicom`);
`vendor_binary_scan.py` is stdlib-only.

Exit codes: **0** clean (or informational notes only) · **1** gating findings ·
**2** usage or environment error. Both **fail closed** — anything they cannot
confidently scan is a finding, not a pass. A `2` is not a pass either; fix the
environment and re-run.

These are the *submission gate*. The prevention layer — the desktop app, the
pre-commit hook, the `.gitignore` work — is
[Step 0](01-repo-hygiene.md), and you should have done it long before now.

## Wire the checks into your own CI (recommended)

Copy the three workflow templates from
[`templates/workflows/`](https://github.com/medphys-code-exchange/index/tree/main/templates/workflows)
in the index repo into your own repo's `.github/workflows/`:

| File | What it does |
|---|---|
| `phi_scan.yml` | PHI scan on every push and PR |
| `vendor_binary_scan.yml` | Vendor-binary / committed-binary scan |
| `submission_lint.yml` | Structure lint: LICENSE, CITATION.cff, README, pinned deps |

Each one pins `SCANNER_REF` to a tagged scanner release rather than a branch —
an unpinned ref makes results irreproducible and would let a change to the
org's default branch silently alter what runs inside your CI. The templates
ship pinned to the current release, so they work as copied. Check
[the releases page](https://github.com/medphys-code-exchange/index/releases)
for a newer tag before you submit; a reviewer may ask you to move to it.

## Test data

R1.5 requires that a stranger can run your worked example. Three acceptable
sources, in rough order of preference:

1. **The Exchange's synthetic phantom dataset** — a deterministic
   CT + RTSTRUCT + RTPLAN + RTDOSE set, generated rather than de-identified, so
   it is clean by construction. Use this if your tool reads RT DICOM.
2. **Your own synthetic data**, bundled in the repo. Generated, not
   de-identified — de-identification is a claim someone has to verify;
   generation is a fact.
3. **Public data** (TCIA or similar), fetched by your example script. Cite the
   collection and pin the version/identifier so the example stays reproducible.

What is never acceptable: real patient data, however thoroughly you believe you
scrubbed it.

## The pre-submission self-check

Work [checklists/pre-submission.md](../checklists/pre-submission.md) until every
box for your tier is ticked. It is keyed to the requirement IDs (R1.1, R2.3,
RC.4, …) so a reviewer's finding maps straight back to a line you can fix.

## Submitting

Open a **Tool Submission** issue in the
[`index`](https://github.com/medphys-code-exchange/index) repo — use the
issue-form template, not a blank issue. It collects:

- Tool name, and your name, email, institution, and (recommended) ORCID
- **Repository URL and the exact commit SHA** you are submitting — the badge
  will certify *that SHA*, so submit the commit you mean, not "whatever `main`
  is today"
- **Release tag** — optional at Tier 1, **required at Tier 2 and Tier C**; the
  tagged release must already exist at review time. Submit the tag's commit,
  not the tip of `main`.
- Requested tier, license (SPDX id), language(s), category, platform matrix
- Test-data source
- Attestations: DCO sign-off, no PHI, no vendor binaries — plus the Tier C
  attestation if you are requesting Tier C

Two things people get wrong:

- **You do not need a DOI to submit.** It is minted at acceptance (Tier 2 and
  Tier C) and back-filled into your `CITATION.cff`. Tier 1 acceptances get an
  index entry and badge, no DOI.
- **The Tier C attestation checkbox is mandatory if you request Tier C.**
  GitHub issue forms cannot make a checkbox conditional, so it is marked
  optional in the form and enforced at editor triage. Leave it unchecked and
  your Tier C submission comes straight back.

## What happens next

1. **Automated checks run** — PHI, vendor binary, structure lint, DCO. Review
   does not start until they are clean. Failures are reported in your issue;
   fix, push, and say so in the thread.
2. **An editor assigns reviewers** — one for Tier 1 and Tier 2 (a second at
   editor discretion), **two for Tier C**, at least one fully independent of
   your institution.
3. **Review happens publicly in your issue thread**, driven by the tier
   checklist. Reviewers tick items, raise concerns as comments, you respond
   with fixes. It reads like a conversation because it is one — this is not a
   silent verdict handed down at the end.
4. **Target turnaround is 30 days** submission → decision, and the program
   tracks and publishes how it actually does against that. Reviewers carry no
   more than 2–3 concurrent reviews so the number stays honest.
5. A submission idle **60 days** awaiting your response is closed as stale.
   That is not a rejection — resubmission is welcome and starts clean.

## Conflicts of interest

Reviewers do not review submissions from their own institution, or from
co-authors and collaborators within the past 4 years. For Tier C, at least one
of the two reviewers must be fully independent; a second, non-independent
reviewer must disclose the relationship in the public thread.

If you are assigned a reviewer you believe is conflicted, say so in the issue.
That is a normal thing to raise, not an accusation.

---

Next: [what acceptance actually gets you](06-after-acceptance.md).
