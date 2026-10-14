# Document Review and Supplied Fixes

Use this reference for explicit document-review or compatibility requests, and for fixes based on supplied findings. Ordinary rewriting uses the [rewrite process](../SKILL.md#process).

Both branches use the mode selected through the [entry point](../SKILL.md#mode-selection) and the [writing policy](writing-rules.md) loaded through its task routing.

## Review workflow

1. **Set scope.** Identify the requested assessment, allowed changes, and requested artifacts. Use available readable text and existing location labels. Preserve the source unless the user requested changes to it. If content is unavailable or incomplete, state the limitation and restrict coverage claims to what you could read. Input-format tooling and extraction validation are outside this workflow.
2. **Read all content.** Read from beginning to end before preparing findings. Include headings, questions, labels, options, definitions, examples, and table text. Keep a compact internal section checklist. Complete this step only when every available part is accounted for. Keep unchanged units off the public report.
3. **Assess in context.** Apply the loaded writing policy to every available unit. Include meaning, idioms, figurative expressions, terminology, and incomplete or ambiguous definitions in the assessment.
4. **Use lint as supplementary evidence.** If run, interpret `scripts/ste-lint.py` through the policy's [evidence limits](writing-rules.md#evidence-and-verification-limits) and [word-choice criteria](writing-rules.md#word-choice).
5. **Prepare actionable findings.** Use the report contract below. Identify the rule or contextual basis for each concern. When meaning or applicability is uncertain, retain the concern as Borderline with a conditional edit or specific author decision. Leave acceptable text and unrelated polishing out.
6. **Check fidelity and publish once.** Compare each proposed edit with its source once using the [source-fidelity policy](writing-rules.md#source-fidelity). Verify quotations and locations against the source. Repair any mismatch before publishing one result. Save only requested artifacts, and identify each saved output by its exact absolute path.

One invocation may include reading, analysis, lint, and the bounded fidelity check. It is not limited to one tool call. Finish after publishing the result. Do not recursively invoke this skill, regenerate reports to meet a score, start a reviewer/optimizer loop, or automatically continue from your own findings. Unresolved author choices stay in the report. Further iteration belongs to the user's AI tool through a new user request.

## Report contract

Use this compact table for actionable findings:

| Location | Source expression | Status | Reason / basis | Suggested edit or author decision |
|---|---|---|---|---|

**Confirmed** means an observable conflict with an identified rule, or a lexical conflict supported by a verified word restriction in the bundled reference or an authoritative entry.

**Borderline** means a contextual concern whose intended meaning, rule applicability, or lexical status remains uncertain. Label every such entry individually. Explain exactly what is uncertain, then give a conditional suggestion or ask for a specific author decision. One general disclaimer does not replace these labels.

Status expresses evidential certainty, not severity. State the applicable [evidence limitation](writing-rules.md#evidence-and-verification-limits) once, including whether authoritative dictionary entries were available.

Each entry must contain a real edit or a specific unresolved decision. Use existing headings, section IDs, line ranges, or page labels. Quote source text accurately, allowing only whitespace normalization for wrapped text. Do not invent locations.

Omit acceptable text, "no rewrite needed" commentary, and duplicate public coverage registers. If there are no actionable findings, state that briefly, subject to the coverage and dictionary limitations. A review report is not a whole-document rewrite.

## Supplied-fixes branch

Use supplied findings as the complete scope, rather than starting the review workflow's full-content audit. Apply step 1's source-edit boundary. Use the source to verify each supplied quotation, its context, and its location.

Give one proposed fix or unresolved author decision per supplied finding using the report table. Retain finding IDs, Confirmed/Borderline status, uncertainty, and conditional assumptions. If source evidence disproves a quotation or basis, identify the discrepancy rather than inventing a matching passage or forcing a fix.

Correct demonstrably mistaken locations and explicitly identify each correction. A corrected location does not change evidential status. Keep unrelated source passages outside the suggestions, even if another possible issue is visible.

Finish with step 6 of the review workflow and its publication boundary, without running the full-content audit.
