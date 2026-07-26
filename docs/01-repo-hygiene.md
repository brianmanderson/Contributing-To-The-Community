# Step 0 — Repository hygiene: no PHI, no vendor binaries

Everything else in this guide is optional in the sense that a rejected
submission can be fixed and resubmitted. This page is not. A PHI leak is not a
review finding; it is a reportable privacy incident at your institution, and it
is permanent in a way a bad README is not.

## The rule

> **Scan and ignore first. Commit second. Push last.**

Once a file is committed it lives in git history until the history is
rewritten. Once it is pushed, it has left your institution. A `.gitignore`
added afterwards un-commits nothing. Every control worth having runs **on your
machine, before the first commit**.

## Use the existing guide — we did not rewrite it

The complete, step-by-step version of Step 0 lives in a separate public repo:

### 👉 [github.com/brianmanderson/CreatingGithubRepoInstructions](https://github.com/brianmanderson/CreatingGithubRepoInstructions)

| What you need | Where it is in that repo |
|---|---|
| Take an existing folder → GitHub repo, safely (GitHub Desktop *and* command-line paths) | [docs/creating-a-repo.md](https://github.com/brianmanderson/CreatingGithubRepoInstructions/blob/main/docs/creating-a-repo.md) |
| **PHI Scan desktop app** — double-click `.exe`, no Python, no terminal | [Releases](https://github.com/brianmanderson/CreatingGithubRepoInstructions/releases) · [csharp/README.md](https://github.com/brianmanderson/CreatingGithubRepoInstructions/blob/main/csharp/README.md) |
| The same scanner as a Python script (for the terminal, hooks, CI) | [tools/phi_scan.py](https://github.com/brianmanderson/CreatingGithubRepoInstructions/blob/main/tools/phi_scan.py) |
| How to *think* about a `.gitignore` instead of copying one | [docs/mindful-gitignore.md](https://github.com/brianmanderson/CreatingGithubRepoInstructions/blob/main/docs/mindful-gitignore.md) |
| A ready medical-project `.gitignore` | [templates/medical-project.gitignore](https://github.com/brianmanderson/CreatingGithubRepoInstructions/blob/main/templates/medical-project.gitignore) |
| Pre-commit hook that blocks a commit on findings | [templates/pre-commit](https://github.com/brianmanderson/CreatingGithubRepoInstructions/blob/main/templates/pre-commit) |
| Branch protection: nothing merges to `main` unless the scan passes | [docs/pr-workflow.md](https://github.com/brianmanderson/CreatingGithubRepoInstructions/blob/main/docs/pr-workflow.md) |
| Why the tooling is shaped the way it is (Action vs. desktop app vs. LLM review) | [docs/phi-scanner-options.md](https://github.com/brianmanderson/CreatingGithubRepoInstructions/blob/main/docs/phi-scanner-options.md) |
| A prompt for having Claude reason about borderline findings | [prompts/phi-review-prompt.md](https://github.com/brianmanderson/CreatingGithubRepoInstructions/blob/main/prompts/phi-review-prompt.md) |

**Read it, run its scanner on your project folder, fix what it finds, and only
then continue here.**

Two notes on reading it as an outside contributor:

1. It was written for a UC San Diego team, so it references a local project
   catalog (`ucsd-catalog` topic) and says to notify Brian on an incident. The
   method and tooling are institution-agnostic; **substitute your own
   institution's privacy-incident reporting process** — yours starts on
   discovery, same as UCSD's.
2. It defaults to **private** repositories, correctly: private-by-default is
   the right posture while you are still finding out what is in your folder.
   Exchange submissions must end up **public** — which raises the stakes on
   this step, it does not lower them. Do not flip a repo public until a clean
   scan and your own read of `git ls-files` say it is safe.

## Two scanners, two different jobs

You will encounter a `phi_scan.py` in both projects. They are not duplicates —
they run at different moments for different reasons, and you want both.

| | **Author-side scanner** (CreatingGithubRepoInstructions) | **Submission scanner** (Exchange `index` repo) |
|---|---|---|
| Runs | On your machine, before the first commit; then every commit via the hook | On a submitted repository, in CI and at intake triage |
| Purpose | **Prevention** — stop PHI from ever entering git | **Gating** — refuse to review a repo that is not demonstrably clean |
| Output | HIGH / MEDIUM / REVIEW findings, `.gitignore`-aware, can write the ignores for you | Exit code 0 clean / 1 gating findings / 2 error, plus `--json` |
| Front end | Desktop GUI (recommended) or script | Script only; never echoes file contents, so CI logs cannot leak PHI |
| Fails on unreadable files? | Flags them **REVIEW** for you to open | **Fails closed** — an unscannable file (archive, Office doc, unparseable DICOM) is a finding, not a pass |

Run the author-side one **first and often**. The submission scanner is the
tollbooth, not the seatbelt: by the time it runs, the code is already on
GitHub. Layer them exactly the way
[phi-scanner-options.md](https://github.com/brianmanderson/CreatingGithubRepoInstructions/blob/main/docs/phi-scanner-options.md)
describes — local scan → pre-commit hook → Action → human/LLM judgment on the
borderline cases.

Expect the submission scanner to be **stricter**. Two differences bite most
often:

- **Archives and Office documents are findings, not warnings.** It never looks
  inside a `.zip`, `.xlsx`, or `.docx` — so it cannot clear one. Unpack it,
  convert it, or remove it.
- **Bundled DICOM must be genuinely anonymized**, not just filename-scrubbed.
  It reads patient-identifying tags (`PatientName`, `PatientID`,
  `PatientBirthDate`, `ReferringPhysicianName`, `InstitutionName`, and more)
  and flags any that are populated. See
  [05-submitting.md](05-submitting.md) for where to get test data that is
  clean by construction.

## Vendor binaries: never committed, no exceptions

ESAPI and RayStation scripts are **fully in scope** for the Exchange — a large
share of the code physicists actually re-implement is vendor-API code, and
excluding it would gut the value of the index. What is not in scope is
redistributing the vendor's assemblies.

- **Never commit** `VMS.TPS.Common.Model.API.dll`, `VMS.TPS.Common.Model.Types.dll`,
  any other `VMS.*` assembly, RayStation `.dll`s, or vendor installers.
  Reference them from the local install path.
- Copy [gitignore_esapi.template](https://github.com/medphys-code-exchange/index/blob/main/templates/gitignore_esapi.template)
  into your repo as `.gitignore` (or merge it into the medical-project one) —
  it covers the usual `bin/`, `obj/`, and vendor-reference paths.
- **Declare your platform matrix** — tested Eclipse/ESAPI or RayStation
  versions are *required* metadata, not a nicety. A vendor script without
  declared versions is unreviewable, because "works" is meaningless without
  saying against what.
- The `vendor_binary_scan.py` check is fail-closed and gating, same as the PHI
  scan.

> **RayStation submitters — read before you submit.** Whether RaySearch's terms
> permit redistribution of certain script patterns is an **open question the
> program has not yet resolved**; RaySearch is being contacted directly. Your
> submission is welcome and will be queued, but acceptance of the first
> RayStation tool waits on that answer. Say "RayStation" in your intake issue
> so it is routed correctly.

## Where data should live

Not next to your code. The layout that makes accidents impossible:

```
C:\Users\you\Projects\MyTool\        ← the repo: code, docs, config only
C:\Users\you\ProjectData\MyTool\     ← data lives here, outside the repo entirely
```

If data must sit beside the code, put **all** of it in one `data/` folder and
ignore that folder wholesale. Your worked example (required at every tier —
R1.5) should use **synthetic or public data**, either bundled or fetched by the
example script. See [05-submitting.md](05-submitting.md#test-data).

## If PHI was committed anyway

Follow the incident section of the source guide —
[creating-a-repo.md § If PHI was committed anyway](https://github.com/brianmanderson/CreatingGithubRepoInstructions/blob/main/docs/creating-a-repo.md#if-phi-was-committed-anyway).
The short version:

- **Committed, not pushed:** nothing has left your machine. Do not just delete
  the file — it is still in history. Reset back past the bad commit, remove or
  ignore the file, re-commit.
- **Already pushed:** treat it as a potential breach, not an engineering
  problem. Report it through your institution's process *first*. Make the repo
  private immediately if it was public. History rewriting and cache purging
  come after reporting, not instead of it. **Do not open an Exchange
  submission for that repository** until your institution has closed it out.

Nobody at the Exchange will penalize you for reporting this. Quietly
force-pushing over it is the thing that goes badly.
