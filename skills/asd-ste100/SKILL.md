---
name: asd-ste100
description: "Review documents for ASD-STE100 compatibility, suggest fixes from supplied findings, or rewrite English that is dense or easy to misparse. Use for tool descriptions, error messages, inter-agent instructions, system prompts, and status reports where misreading has a real cost. Triggers: STE100 review, disambiguate, apply Simplified Technical English, plain-language rewrite, controlled-language rewrite, rewrite so an agent cannot misread this. Not for creative or marketing copy, or persuasive copy where voice, nuance, or persuasion is the point."
metadata:
  version: "0.4.0"
---

# Simplified Technical English (ASD-STE100)

## Task Routing

Before assessing or rewriting text, read [references/writing-rules.md](references/writing-rules.md). It owns the language rules, mode-dependent enforcement, source fidelity, and verification policy for every branch.

- **Document review or compatibility assessment:** Read [references/review-workflow.md](references/review-workflow.md) and follow its review workflow and report contract.
- **Suggested fixes from supplied findings:** Read the same reference and follow its supplied-fixes branch.
- **Rewriting:** Follow the Process and Output Format below, using ordinary task inference.

## Mode Selection

Use the user's mode choice when supplied. Otherwise, infer it from the text type:

- **Strict:** procedures, error messages, tool and function descriptions, inter-agent instructions, and safety text. Use it wherever a wrong reading has a cost.
- **STE-flavored:** READMEs, PR descriptions, changelogs, and explanatory prose.

## Process

This is the rewrite path. Review and supplied-fixes tasks use the reference selected in Task Routing.

1. Select the mode using Mode Selection.
2. Read the input text once for meaning — do not start rewriting before you understand what it must still say afterward.
3. Walk the input sentence by sentence. Flag every rule violation and scan concern in the loaded policy, using its [mode-dependent enforcement](references/writing-rules.md#mode-dependent-enforcement). For a mechanical first pass, run `scripts/ste-lint.py`. Use `--help` for its interface and apply the [evidence limits](references/writing-rules.md#evidence-and-verification-limits).
4. Rewrite each flagged sentence using the [source-fidelity policy](references/writing-rules.md#source-fidelity).
5. Output the result using Output Format.
6. If the input already complies, say so — do not force changes onto compliant text.

## Output Format

**Default: the rewritten text, and nothing else.** Most callers want a result they can paste straight into a tool description, an error string, or a prompt. Print the simplified text on its own. Do not add a preamble about this skill, a mode announcement, a violation count, a summary of what changed, a rule table, or a closing offer to explain further.

The one permitted addition: if step 4 kept a longer phrasing on purpose, add a single line after the text, prefixed `Kept as-is:`, naming the phrase and the precision that would have been lost. Omit the line when there is nothing to report.

**On request: the rule table.** When the user asks to see the reasoning — "show the diff", "which rules did it break", "explain the changes", "before/after" — output this table instead:

```markdown
| Rule violated | Original | Simplified |
|---|---|---|
| <Rule name> | "<Original text>" | "<Simplified text>" |

Mode: <Strict or STE-flavored>. <Count> violations found.
```

Follow the table with a one-line note on anything you deliberately did **not** simplify, and why (usually: simplifying would lose required precision). Explain the applicable evidence limitation when giving requested reasoning.

## Additional Resources

- [examples/before-after.md](examples/before-after.md) — worked rule applications, agent-output rewrites, and contextual review demonstrations. Consult it when a concrete example would help.
