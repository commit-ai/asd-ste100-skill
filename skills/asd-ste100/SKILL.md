---
name: asd-ste100
description: "Use to rewrite instructions and operational technical text: procedures, tool/function contracts, error messages, and agent instructions. These define actions, conditions, constraints, or failure behavior. Also use for explicit ASD-STE100 or Simplified Technical English requests, including document reviews and fixes from supplied STE findings. For other text, require an explicit STE request. Requests to clarify, explain, rephrase, or shorten open questions, discussion, or general prose do not trigger this skill on their own."
metadata:
  version: "0.4.0"
---

# Simplified Technical English (ASD-STE100)

## Task Routing

Check scope first. Automatic use requires instructions or operational technical text as defined in the description. Judge the text's function, not its file type or audience. A README can contain a procedure. A message to an agent can be ordinary discussion. For other text, proceed only when the user explicitly requests STE or names this skill. Otherwise, handle the request normally, without applying this skill's rules or output contract.

Before assessing or rewriting text, read [references/writing-rules.md](references/writing-rules.md). It owns the language rules, mode-dependent enforcement, source fidelity, and verification policy for every branch.

- **Document review or compatibility assessment:** Read [references/review-workflow.md](references/review-workflow.md) and follow its review workflow and report contract.
- **Suggested fixes from supplied findings:** Read the same reference and follow its supplied-fixes branch.
- **Rewriting:** Follow the Process and Output Format below, using ordinary task inference.

## Mode Selection

After the scope check, use the user's mode choice when supplied. Otherwise, infer it from the text type:

- **Strict:** procedures, error messages, tool and function descriptions, inter-agent instructions, and safety text.
- **STE-flavored:** other prose admitted by an explicit STE request, such as README explanations, PR descriptions, and changelogs.

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
