# open-h-4dphysio-shared

Support material read by the other Open-H-4DPhysio skills. **Not an invocable skill** —
it deliberately has no `SKILL.md`, so `scripts/bootstrap_skills.py` gives it no
entry under `.claude/skills/` and no agent tries to invoke it.

| File | What it is |
|---|---|
| [`layout-spec.md`](layout-spec.md) | **Normative.** The submission layout: naming grammar, directory structure, sidecar schemas, RFP conformance rules. Every skill reads this. |
| [`cfp-summary.md`](cfp-summary.md) | The Open-H-4DPhysio CFP condensed: scope, review criteria, governance, timeline, steering group. |
| [`data-card-template.md`](data-card-template.md) | What the submission's `README.md` must contain, including the Hugging Face YAML frontmatter. |
| [`patient-json-template.json`](patient-json-template.json) | Annotated example of every `patient.json` field. |
| [`study-json-template.json`](study-json-template.json) | Annotated example of every `study.json` field. |
| [`phi-checklist.md`](phi-checklist.md) | The 18 HIPAA Safe Harbor identifiers and where each hides in imaging data. |
| [`evaluation-report-template.md`](evaluation-report-template.md) | The exact structure of `evaluation_report.md`. |

## The prose and the code must agree

`layout-spec.md` is what contributors read. `src/open_h_4d_physio/` is what actually
enforces the rules. If they disagree, a contributor is told one thing and graded
on another.

`tests/test_spec_consistency.py` makes that a CI failure rather than a surprise:
it extracts the three regexes from the grammar block in `layout-spec.md` and
asserts they are character-for-character identical to the patterns compiled in
`open_h_4d_physio.naming`, checks that both JSON templates validate against their schemas,
and checks that every conformance rule the code can emit is documented in the
spec's rule table.

So editing a rule means editing both places. That is the intended friction.

## Referring to these files

Skills use relative paths — `../open-h-4dphysio-shared/layout-spec.md`. That resolves
identically whether `.claude/skills/<name>` is a symlink, a Windows directory
junction, or a plain copy, which is why the bootstrap's fallback chain is safe.
