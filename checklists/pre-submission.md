# Pre-submission self-check

Work this list until every box for your tier is ticked. Items are keyed to the
requirement IDs in [docs/02-tiers.md](../docs/02-tiers.md), so a reviewer's
finding maps straight back to a line here.

Copy this into your intake issue if you like — reviewers appreciate seeing it
worked.

---

## Step 0 — Safety (everyone, before anything else)

- [ ] I ran the **author-side PHI scanner** on my project folder — the
      [desktop app](https://github.com/brianmanderson/CreatingGithubRepoInstructions/releases)
      or [`tools/phi_scan.py`](https://github.com/brianmanderson/CreatingGithubRepoInstructions/blob/main/tools/phi_scan.py) —
      and resolved every HIGH, MEDIUM, and REVIEW finding.
- [ ] Patient data lives **outside** the repo folder (or entirely inside one
      wholesale-ignored `data/`).
- [ ] `git ls-files` shows only code, docs, and config. I read the whole list.
- [ ] My `.gitignore` is one I have actually read and pruned, not one I pasted.
      ([mindful-gitignore.md](https://github.com/brianmanderson/CreatingGithubRepoInstructions/blob/main/docs/mindful-gitignore.md))
- [ ] No vendor binaries anywhere in the tree or the history — no `VMS.*.dll`,
      no RayStation assemblies, no vendor installers.
- [ ] Nothing in history I would not want public. (If there is: stop, and read
      [01-repo-hygiene.md § If PHI was committed anyway](../docs/01-repo-hygiene.md#if-phi-was-committed-anyway).)

## Tier 1 — required for every submission

- [ ] **R1.1 README** — purpose, installation steps, and **one fully worked
      example a stranger can run end to end**. I tested it from a clean clone.
- [ ] **R1.2 License** — `LICENSE` (or `LICENSE.txt` / `LICENSE.md` /
      `COPYING`) at the repo root, OSI-approved, copyright line filled in.
- [ ] **R1.3 Citation** — valid `CITATION.cff`
      ([template](../templates/CITATION.cff.template)); validated, e.g. with
      [cffconvert](https://github.com/citation-file-format/cffconvert).
- [ ] **R1.4 Pinned dependencies** — `requirements.txt` with versions, `.csproj`
      with package versions, or an equivalent lockfile.
- [ ] **R1.5 Example data** — synthetic or public, bundled or fetched by the
      example, enough to run it. **No PHI.**
- [ ] **R1.7 Submission scanners clean** — `python phi_scan.py .` and
      `python vendor_binary_scan.py .` both exit **0**. (Exit 2 is an
      environment error, not a pass.)
- [ ] **R1.8 DCO** — every commit in the submitted range carries
      `Signed-off-by`. I have the right to release this code
      ([04-ip-and-dco.md](../docs/04-ip-and-dco.md)).
- [ ] The sign-off address is **verified on my GitHub account** — any domain
      (Gmail, Yahoo, university, my own) is fine, but it must be confirmed on
      the account. Checked by opening one of my commits on GitHub and seeing
      my avatar and a clickable username next to it.
- [ ] I am submitting a **specific commit SHA**, and it is the one I mean.

*(R1.6, the reviewer sanity pass, is not yours to tick — but you can make it
easy by having actually run your own worked example from a clean clone.)*

## Tier 2 — everything above, plus

- [ ] **R2.1 Tests** — a suite exercising core functionality, **passing in CI
      on the exact commit I am submitting**.
- [ ] **R2.2 Documentation** beyond the README — docstrings plus generated
      docs, a `docs/` directory, or equivalent.
- [ ] **R2.3 Tagged release exists now**, matching the submitted commit. I am
      submitting the tag's commit, not the tip of `main`. (No DOI needed yet —
      it's minted at acceptance.)
- [ ] **R2.4 Platform matrix declared** — language runtime, key dependency
      versions, and for vendor-API code the vendor platform versions
      (e.g. "Python 3.12" or "Eclipse 18.0 / ESAPI 18.0").
- [ ] CI workflows wired up from [templates/workflows/](../templates/workflows/),
      with `SCANNER_REF` pinned to a tagged scanner release (not a branch).

## Tier C — clinical-adjacent: everything above, plus

Tier C is **Tier 2 mandatory**. A Tier C tool that only meets Tier 1 is
rejected, not down-tiered.

- [ ] **RC.1 Validation dataset** — bundled inputs with known-correct outputs
      **and tolerances**, so an adopting site can verify local reproduction.
- [ ] **RC.2 Site-commissioning checklist** — what an adopting site must run
      and which numbers to confirm before clinical use.
- [ ] **RC.3 Versioned-use statement** — README states prominently that
      clinical use is supported only from tagged releases, never from `main`.
- [ ] **RC.5 Intended-use statement** — explicit about what the tool is and is
      **not** for; framed as a reference implementation requiring local
      commissioning.
- [ ] I ticked the **Tier C attestation checkbox** on the intake form. (It is
      marked optional there only because GitHub issue forms cannot make a
      checkbox conditional. Unticked Tier C submissions are returned at triage.)

*(RC.4 — two reviewers, at least one fully independent of your institution — is
the editor's to arrange. Listing your institution and recent co-authors
accurately in the intake form is what makes it possible.)*

## Last look before you open the issue

- [ ] I cloned my repo fresh into an empty directory, followed my own README
      from the top, and the worked example ran.
- [ ] The commit SHA in my intake issue matches what I just tested.
- [ ] Repository is **public**, or will be at review time.
