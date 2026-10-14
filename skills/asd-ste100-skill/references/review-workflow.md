# Document Review and Supplied Fixes

Use this reference for explicit document-review or compatibility requests, and for fixes based on supplied findings. Ordinary rewriting uses the [rewrite process](../SKILL.md#process).

Apply the existing Strict or STE-flavored writing policy. Assess instructions against the 20-word cap and descriptions against the 25-word cap. Count complete sentences despite visual wrapping.

## Review workflow

1. **Set scope.** Identify the requested assessment, allowed changes, and requested artifacts. Use available readable text and existing location labels. Preserve the source unless the user requested changes to it. If content is unavailable or incomplete, state the limitation and restrict coverage claims to what you could read. Input-format tooling and extraction validation are outside this workflow.
2. **Read all content.** Read from beginning to end before preparing findings. Include headings, questions, labels, options, definitions, examples, and table text. Keep a compact internal section checklist. Complete this step only when every available part is accounted for. Keep unchanged units off the public report.
3. **Assess in context.** Use the [core rules](../SKILL.md#core-rewrite-rules) and [bundled rule reference](writing-rules.md), including its verified word restrictions, technical-terminology criteria, and safety-wording constraints. Check meaning, idioms, figurative expressions, terminology, and incomplete or ambiguous definitions. Distinguish literal uses from idiomatic uses. Assess full sentences across wrapped lines and each table cell in its context.
4. **Use lint as supplementary evidence.** If run, `scripts/ste-lint.py` proposes candidates, not conclusions. Clean lint does not complete a review. A heuristic match is not proof of a violation. Distinguish noun `checks` from verb `verify`, and distinct actions from synonym rotation. Keep established terms rather than renaming them merely to satisfy lint.
5. **Prepare actionable findings.** Use the report contract below. Identify the rule or contextual basis for each concern. When meaning or applicability is uncertain, retain the concern as Borderline with a conditional edit or specific author decision. Leave acceptable text and unrelated polishing out.
6. **Check fidelity and publish once.** Compare each proposed edit with its source once using the fidelity criteria below. Verify quotations and locations against the source. Repair any mismatch before publishing one result. Save only requested artifacts, and identify each saved output by its exact absolute path.

One invocation may include reading, analysis, lint, and the bounded fidelity check. It is not limited to one tool call. Finish after publishing the result. Do not recursively invoke this skill, regenerate reports to meet a score, start a reviewer/optimizer loop, or automatically continue from your own findings. Unresolved author choices stay in the report. Further iteration belongs to the user's AI tool through a new user request.

## Report contract

Use this compact table for actionable findings:

| Location | Source expression | Status | Reason / basis | Suggested edit or author decision |
|---|---|---|---|---|

**Confirmed** means an observable conflict with an identified rule, or a lexical conflict supported by a verified word restriction in the bundled reference or an authoritative entry.

**Borderline** means a contextual concern whose intended meaning, rule applicability, or lexical status remains uncertain. Label every such entry individually. Explain exactly what is uncertain, then give a conditional suggestion or ask for a specific author decision. One general disclaimer does not replace these labels.

Status expresses evidential certainty, not severity. State the official-dictionary limitation once, including whether authoritative entries were available. The bundled restrictions support only their stated word facts, not a complete dictionary audit. If neither a bundled fact nor an authoritative entry covers the intended use, leave approval or prohibition unverified. Never invent an entry or claim certified compliance.

Each entry must contain a real edit or a specific unresolved decision. Use existing headings, section IDs, line ranges, or page labels. Quote source text accurately, allowing only whitespace normalization for wrapped text. Do not invent locations or expansions of undefined terms.

Omit acceptable text, "no rewrite needed" commentary, and duplicate public coverage registers. If there are no actionable findings, state that briefly, subject to the coverage and dictionary limitations. A review report is not a whole-document rewrite.

## Fidelity criteria

Preserve actors, actions, objects, alternatives, selection counts, examples, timing, modality, conditions, and human approvals. Preserve documentation and applicability claims separately from claims about actual practice. Keep recommendations as recommendations, design intentions as intentions, and permission as permission.

Do not supply new troubleshooting steps, mechanisms, architecture, measurements, or certainty. Preserve necessary precision even when a length cap cannot be met. When an equivalent fix is unsupported, report the unresolved issue instead of silently changing the meaning.

## Supplied-fixes branch

Use supplied findings as the complete scope, rather than starting the review workflow's full-content audit. Use the source to verify each supplied quotation, its context, and its location.

Give one proposed fix or unresolved author decision per supplied finding using the report table. Retain finding IDs, Confirmed/Borderline status, uncertainty, and conditional assumptions. If source evidence disproves a quotation or basis, identify the discrepancy rather than inventing a matching passage or forcing a fix.

Correct demonstrably mistaken locations and explicitly identify each correction. A corrected location does not change evidential status. Keep unrelated source passages outside the suggestions, even if another possible issue is visible.

Apply the same fidelity check and artifact rules, then publish one result. Leave source files unchanged unless the user explicitly requested edits.
