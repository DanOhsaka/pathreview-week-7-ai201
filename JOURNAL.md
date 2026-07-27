# Module 3 Journal

## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/147

**Issue title:** Resume section detection fails on text with leading whitespace

**Tier:** [x] Tier 1  [ ] Tier 2  [ ] Tier 3

**Problem summary:**
Section detection in `ingestion/parsers/resume_parser.py` looks for headers like `Education` and `Skills` only when they sit at the very start of a line. PDF-extracted resumes often keep indentation, so those headers never match and `detected_sections` comes back empty even when the sections are clearly present. A successful fix should allow optional leading whitespace in the header regex patterns so indented resumes still report the right sections, and the related unit tests in `tests/unit/test_resume_parser.py` should pass.

**"Is this right for me?" checklist / selection notes:**
- Scope is small and localized to `_detect_sections()` regex patterns — good first contribution.
- Tier 1 / good-first-issue label matches my current level for Module 3.
- Clear reproduce steps and named failing tests make success criteria easy to verify.
- Touches the ingestion subsystem without requiring frontend, agent, or RAG changes.

**Branch name:** fix/147-resume-section-whitespace

**Setup confirmation:** [x] App runs locally at localhost:5173

**Cohort ledger:** [x] Issue added to cohort ledger

## Week 8 — Reproduction & solution planning

**Reproduction commit link:** https://github.com/DanOhsaka/pathreview-week-7-ai201/commit/06591db977b1f934049e0ef1148ac6c33f91efe0

**Reproduction summary:**
I ran the exact indented resume sample from issue #147 through the old `_detect_sections` regexes (no `\s*` after `^`/`\n`) and got `detected_sections: []`, then compared that to the current parser which returns Education and Skills. That comparison is checked in as `scripts/reproduce_issue_147.py` plus a docstring on `_detect_sections` explaining the failure mode.

**PLAN.md link:** https://github.com/DanOhsaka/pathreview-week-7-ai201/blob/fix/147-resume-section-whitespace/PLAN.md

**Walkthrough video (recommended):** 

**Blockers or open questions:**
None for the core fix. Optional follow-up: whether multi-line PDF headers (header split across lines) need a separate issue; out of scope for #147.
