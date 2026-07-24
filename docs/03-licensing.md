# Step 2a — Licensing

A `LICENSE` file with an **OSI-approved** license is a hard requirement at
every tier. No exceptions, and no "free for academic use" — that is not an
open-source license, and code carrying it cannot be indexed.

## The policy

- **Any OSI-approved license is accepted.** Pick from the
  [OSI list](https://opensource.org/licenses); if it isn't on that list, it
  doesn't qualify.
- **The license is first-class index metadata.** It is displayed on your entry
  and badge *before* anyone downloads anything. Nobody should discover your
  license terms after integrating your code.
- **Recommended for new code: Apache-2.0.** Its explicit patent grant matters
  in medical software in a way it doesn't in a web framework. MIT is
  acceptable; Apache-2.0 is better.
- **Copyleft (GPL/AGPL) is accepted but flagged visibly** on your index entry.
  This is not a judgment about copyleft — it's that hospital legal review
  frequently blocks copyleft adoption, and users need to see that before they
  build on your work rather than after.
- **Relicensing is never required.** You own your repository; the frozen fork
  carries the license exactly as reviewed.
- **Mixed licenses** — if you vendor third-party code, document every component
  license in your README. The entry shows your primary license plus a
  "contains mixed licenses" flag.

## Choosing, in one paragraph

If you are writing new code and have no constraint pushing you elsewhere, use
**Apache-2.0**. If your institution's tech-transfer office has a house
preference, use theirs — the fight is not worth it, and every OSI license is
accepted here. If your tool links GPL dependencies, you likely have to be GPL
too; that is fine, it will just be flagged.

## Getting the file right

Copy the full license text into a file named `LICENSE` (or `LICENSE.txt`,
`LICENSE.md`, or `COPYING` — the structure lint accepts all of these) at the
repo root. Fill in the copyright line with the year and the copyright holder —
which, if your employer owns the work, is **your institution, not you**. See
[04-ip-and-dco.md](04-ip-and-dco.md) before you decide which.

GitHub will do this for you: **Add file → Create new file → name it `LICENSE`**
and a license-picker appears.

## What the license does not do

It does not settle whether you had the right to release the code in the first
place. That's the next page.
