# CHECKLIST.md — wiring the NeurIPS Paper Checklist

*Drop from the build-pipeline owner, 2026-05-06. Archive this file under `_archive/` once the checklist is wired and filled in.*

---

The NeurIPS Paper Checklist is required — a paper without it gets desk-rejected. Your paper currently has no `src/checklist.tex` and no `Checklist`-typed manifest row. The build pipeline supports the wiring (proven on 00-test-paper and 02-unified-convergence-rl); what's left is per-paper-agent work. Recipe below.

## Why each paper owns its own copy

The checklist requires *filled-in answers per paper* — different papers answer differently, especially on Reproducibility / Code / Data (theory papers often `\answerNA{}` with one-line justifications) and Limitations / Societal Impact. So this isn't a "build pipeline auto-injects one canonical form" situation — each paper takes the canonical template, fills it in, and ships its own copy.

## Recipe

**1. Copy the canonical template.**

```bash
cp ../common/checklist.tex src/checklist.tex
```

(`common/checklist.tex` is the canonical NeurIPS 2026 form, 250 lines.)

**2. Delete the instruction block.**

The canonical itself instructs you to do this — *"Delete this instruction block, but keep the section heading 'NeurIPS Paper Checklist'."* In `src/checklist.tex`, remove lines 3–29 (everything between `%%% BEGIN INSTRUCTIONS %%%` and `%%% END INSTRUCTIONS %%%`, inclusive of those marker lines). Keep the `\section*{NeurIPS Paper Checklist}` heading at the top.

**3. Fill in every answer.**

Replace each `\answerTODO{}` with one of `\answerYes{}`, `\answerNo{}`, `\answerNA{}`. **Every answer needs a 1–2 sentence justification immediately after the answer macro** — even `\answerNA{}`. The canonical's framing: *"\answerNA{} means either that the question is Not Applicable for that particular paper or the relevant information is Not Available."* For a theory paper, expect `\answerNA{}` to appear frequently in Reproducibility / Code / Data / Compute; that's expected and fine, just give a one-line justification.

Don't modify the questions themselves or the guideline bullets under each. Only edit the answer macros + justification text.

For `\answerYes{}` answers, point to the section(s) of your paper that contain the relevant material — e.g., `\answerYes{} The main contributions are stated in §1 (introduction) and Theorem 4.1, which exactly matches the abstract's claim.`

**4. Add the manifest row.**

In `OUT.llm-hallucinate-neurips-2026.md`, append as the **last** row of the assembly table (after Bibliography and Appendix rows — single-PDF order per AUTHORING §5.2):

```
| – | Checklist | [checklist](src/checklist.tex) | NeurIPS paper checklist | <stage> |
```

Section column is `–` (em-dash; checklist isn't a numbered section). Stage is your call (`draft` / `restructure-draft` / `ready` / etc.).

If you have other manifests that shouldn't have the checklist, leave them alone — the rule is *every submission-bound manifest needs a Checklist row*, not every manifest.

## What the build does

- Auto-injects `\newpage` before any `Checklist`-typed segment (so the checklist always starts on a fresh page).
- Renders raw `.tex` segments verbatim — no kramdown processing.
- Page-budget reports the checklist as part of the appendix-bib region, not the 9-page main-text budget. (References, optional appendices, and the checklist do not count toward the 9-page limit per AUTHORING §5.1.)

## When you're done

Archive this file: `git mv CHECKLIST.md _archive/CHECKLIST-2026-05-06.md` (preserves git history), and check off the corresponding TODO entry.

## References

- AUTHORING.md §1.12 (Checklist segment authoring) + §5.2 (single-PDF order) + §5.5 (filling in what you know) + §5.7 (appendix vs body content scope).
- `common/checklist.tex` — canonical NeurIPS 2026 template, 250 lines, full multi-question form.
- `02-unified-convergence-rl/src/checklist.tex` — worked example (224 lines; 02's agent has trimmed the instruction block + is filling in answers).
- `00-test-paper/src/checklist.tex` — minimal stub showing manifest wiring works.
