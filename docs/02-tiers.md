<!--
  NORMATIVE, CONTRIBUTOR-FACING COPY of the tier requirements.
  This file is what contributors and reviewers are held to. The design record
  behind it lives in the program planning repo (docs/DECISIONS.md D7 and
  docs/tiers.md). If the two ever disagree they must be reconciled
  deliberately — do not edit one without the other.
-->
# Step 1 — Pick your tier

The badge certifies **a specific commit at a specific tier**. The tier is what
tells a stranger how much to trust it, so pick the one you can actually meet;
requesting a higher tier than your code supports just costs you a review cycle.

Automated checks (PHI, vendor binaries, structure lint, DCO) run **before** any
human reviewer sees the submission. A submission that fails them is returned
without review — that is not a rejection, it is a bounce, and you can fix and
resubmit immediately.

| | **Tier 1** | **Tier 2** | **Tier C** |
|---|---|---|---|
| For | Research code, analysis scripts, utilities, prototypes | Mature tools (the default for anything you'd tell a colleague to use) | Anything whose output could inform a clinical decision |
| Reviewers | 1 | 1 (2nd at editor discretion) | **2**, at least one fully independent |
| Tests in CI | — | Required | Required |
| Tagged release + DOI | — | Required | Required |
| Validation dataset | — | — | Required |

---

## Tier 1 — Research / analysis tools (light bar)

Intended for research code, analysis scripts, utilities, and prototypes. **Not**
for anything whose output feeds a clinical decision.

Everything here is bot-checkable except R1.6.

- **R1.1 README** — purpose statement, installation steps, and at least one
  fully worked example a stranger can run end to end. See
  [../templates/README.template.md](../templates/README.template.md).
- **R1.2 License** — a `LICENSE` file with an OSI-approved license. See
  [03-licensing.md](03-licensing.md).
- **R1.3 Citation** — a valid `CITATION.cff`. See
  [../templates/CITATION.cff.template](../templates/CITATION.cff.template).
- **R1.4 Pinned dependencies** — `requirements.txt` with versions, `.csproj`
  with package versions, or an equivalent lockfile.
- **R1.5 Runnable example data** — synthetic or public data, bundled or fetched
  by the example, sufficient to execute the worked example. **No PHI.**
- **R1.6 Reviewer sanity pass** — one reviewer confirms the worked example runs
  and the code does what the README claims.
- **R1.7 Automated scans pass** — PHI scan and vendor-binary scan clean.
- **R1.8 DCO** — every commit in the submitted range carries `Signed-off-by`,
  using an email address **verified on the signer's GitHub account**. Any
  domain qualifies; verification on the account is what is required. See
  [04-ip-and-dco.md](04-ip-and-dco.md).

## Tier 2 — Rigorous (the default for mature tools)

Everything in Tier 1, plus:

- **R2.1 Automated tests** — a test suite exercising the core functionality,
  passing in CI **on the exact reviewed commit**.
- **R2.2 Documentation** — API or usage documentation beyond the README
  (docstrings plus generated docs, a `docs/` directory, or equivalent).
- **R2.3 Tagged release; DOI at acceptance** — a tagged release corresponding to
  the reviewed commit must exist **at review time**. You do not need a DOI to
  submit: the Zenodo DOI is minted at acceptance through the org's integration
  and back-filled into your `CITATION.cff` and the metadata record.
- **R2.4 Platform matrix** — declared tested versions: language runtime, key
  dependencies, and — for vendor-API code — vendor platform versions
  (e.g. Eclipse 18.0 / ESAPI 18.0).
- **R2.5 Second reviewer** — optional, at editor discretion.

## Tier C — Clinical-adjacent (Tier 2 mandatory, plus additions)

Applies to any tool whose output could plausibly inform a clinical decision:
plan checks, dose calculations, QA analysis, structure evaluation, transfer
checks. **If in doubt, it's Tier C.** A Tier C submission that meets only
Tier 1 quality is rejected, not quietly down-tiered — so don't request Tier 1
for clinical-adjacent code hoping to slip under the bar.

The framing to hold in your head: **a reference implementation requiring local
commissioning.** The badge is not a clinical clearance and never claims to be.

Everything in Tier 2, plus:

- **RC.1 Validation dataset** — bundled input data with known-correct outputs
  and tolerances, so an adopting site can verify the tool reproduces expected
  results locally.
- **RC.2 Site-commissioning checklist** — a document telling an adopting site
  what to run and what numbers to confirm before clinical use, in the spirit of
  TPS commissioning practice.
- **RC.3 Versioned-use statement** — the README states prominently that
  clinical use is supported only from tagged releases, never from `main`.
- **RC.4 Two reviewers** — mandatory. At least **one** must be fully
  independent of your institution (no shared affiliation, no co-authorship with
  you within 4 years). The second may be non-independent but must disclose the
  relationship publicly in the review issue.
- **RC.5 Intended-use statement** — an explicit description of what the tool is
  and is **not** for.

---

## Verification status (all tiers)

Acceptance records the reviewed commit hash, tier, platform matrix, review
issue link, and date. Your badge reads
**"Verified [date] — tested against [platform versions]."**

If verification is not renewed within **24 months**, status flips automatically
to **"Archived — verified as of [date], unverified since."** Renewal is
cheap: a re-run of the scans and CI on the frozen fork, or your own
re-attestation with an updated platform matrix.

**Nothing is ever deleted.** Staleness is disclosed, not erased — a tool that
was good in 2027 and untouched since is still the best starting point somebody
has, as long as they can see that's what they're getting.

## Tier promotion

Tier 1 → Tier 2 is a supported, expected path. Request a re-review against the
Tier 2 requirements; on success the badge and index entry update and a new
frozen fork is cut at the newly reviewed commit. Submitting at Tier 1 first is
a legitimate strategy — get indexed, then earn the higher bar.
