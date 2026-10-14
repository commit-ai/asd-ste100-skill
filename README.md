# ASD-STE100 Skill — Simplified Technical English for Agent Output

A Claude Code skill that reviews documents and rewrites dense, ambiguous English using the discipline of [ASD-STE100 Simplified Technical English](https://www.asd-ste100.org/) (STE) — the controlled-language standard the aerospace and defense industry built so aircraft maintenance instructions cannot be misread.

This skill repurposes that same discipline for a different reader: an **AI agent** parsing another agent's output, a tool description, an error message, or an inter-agent instruction, with no human in the loop to resolve ambiguity.

## Why STE, and Why for Agents

STE exists because a misread instruction on an aircraft can kill people, and the intended readers were often not native English speakers with no author to call for clarification. The standard's fix: one meaning per word, active voice, simple tenses, one instruction per sentence, short sentences, no dropped words.

An LLM agent parsing another agent's output is in a strikingly similar position — no back-channel, no way to ask "did you mean X or Y?" The same rules that keep a mechanic from misreading a torque spec keep a downstream agent from misreading a tool description or an inter-agent message.

## Before / After

| Before | After |
|---|---|
| "This tool will attempt to synchronize state across the various backends that have been configured, and if a conflict is detected it may resolve it automatically depending on the strategy that has been set, or otherwise it will surface the conflict for manual review." | "The tool will try to synchronize state across the configured backends. If a conflict is detected, the tool may resolve it automatically. This possible resolution depends on the configured strategy. Otherwise, it will report the conflict for manual review." |
| "An error may have occurred while processing your request due to a possible mismatch in the expected data format, which could be caused by an outdated client version." | "An error may have occurred while processing your request. A mismatch with the expected data format may be the cause. An outdated client version could cause this mismatch." |

The tool example retains the source's ambiguous "otherwise". The author must clarify whether the fallback covers every unresolved conflict or only a strategy that excludes automatic resolution. The rewrite adds no strategy-reading operation.

These are provisional clarity rewrites, not verified Issue 9-compliant text. The error example retains a compound form and an `-ing` verb under this skill's fidelity policy. Neither that policy nor the local Strict/STE-flavored modes are exceptions or conformance levels defined by ASD-STE100.

More worked rule applications, case-specific explanations, and unresolved choices are in [`skills/asd-ste100/examples/before-after.md`](skills/asd-ste100/examples/before-after.md). They demonstrate the [writing policy](skills/asd-ste100/references/writing-rules.md), rather than defining additional instructions.

## What This Skill Does

The task router separates document review, fixes from supplied findings, and ordinary rewriting. Strict and STE-flavored remain writing policies, not task types.

Each skill file has one responsibility. [`SKILL.md`](skills/asd-ste100/SKILL.md) owns routing, mode selection, and the rewrite workflow/output contract. [`references/writing-rules.md`](skills/asd-ste100/references/writing-rules.md) is the authoritative owner of language rules, shared fidelity constraints, evidence limits, and verification guidance; every task branch loads it before applying rules. [`references/review-workflow.md`](skills/asd-ste100/references/review-workflow.md) owns the review and supplied-fixes workflows and report contract. The examples contain demonstrations and links to those owners.

For rewriting, the skill:

1. Picks a mode. **Strict** covers procedures, error messages, and tool descriptions. **STE-flavored** covers READMEs, PR descriptions, and explanatory prose. STE-flavored keeps the sentence discipline but not the fixed-vocabulary lockdown.
2. Reads the input English text for meaning.
3. Flags every rule violation sentence-by-sentence: ambiguous word choice, present-perfect/complex tense, passive voice with an unclear actor, multi-instruction sentences, oversized noun clusters, dropped words, sentences over length, phrasal verbs, nominalized actions, semicolons, hedge stacks, and marketing adjectives.
4. Rewrites each flagged sentence — without dropping any fact, condition, or scope qualifier from the original. If a shorter phrasing would lose required precision, it keeps the longer phrasing and flags the trade-off instead of silently simplifying.
5. Outputs the rewritten text on its own — no preamble, no mode announcement, no change summary — plus a one-line `Kept as-is:` note when it deliberately left something unsimplified.

Ask for the reasoning ("show the diff", "which rules did it break") and it outputs a before/after table naming each rule instead.

Punctuation and word counts are observable checks. Idiomatic meaning, synonym equivalence, rule applicability, and faithful edits require contextual judgment. Lexical approval remains unverified without authoritative dictionary evidence. STE-flavored treats lexical rules as advisory.

For document review, the skill reads all available content, including headings, questions, options, examples, and table text. It uses an internal section checklist and publishes actionable findings only:

| Location | Source expression | Status | Reason / basis | Suggested edit or author decision |
|---|---|---|---|---|

**Confirmed** identifies an observable rule conflict or a lexical conflict backed by a verified bundled restriction or authoritative entry. **Borderline** marks each concern whose meaning, applicability, or lexical status remains uncertain. Each borderline row explains that uncertainty and gives a conditional edit or specific author decision. Status indicates certainty, not severity.

The review preserves meaning, selection counts, examples, approval conditions, and requirement strength. It distinguishes documented applicable requirements from actual practice. It states the dictionary limitation once and does not list acceptable text as findings. If source content is incomplete, it states the coverage limitation.

For suggested fixes, supplied findings define the scope. The skill preserves their statuses and assumptions, verifies quotations and locations, and explicitly corrects proven location errors without starting a new audit. It saves only requested artifacts and identifies saved outputs by exact absolute path.

Each invocation ends with one result after a bounded fidelity check. The skill does not recursively invoke itself, optimize reports to a score, or start automatic follow-up reviews. Further iteration belongs to the user's AI tool. Full branch instructions: [`skills/asd-ste100/references/review-workflow.md`](skills/asd-ste100/references/review-workflow.md).

The linter checks structural patterns only. It does not compare an original text with a rewrite, verify that requirement strength stayed the same, or prove that the rewrite preserved meaning. A zero-violation result means that the configured structural checks found no problems, not that a document review is complete. A heuristic finding is a candidate, not proof. For example, noun `checks` and verb `verify` need not name the same action.

The deterministic linter checks semicolons, a short list of soft phrasal verbs (spin up, reach out, dive into, kick off, circle back, touch base), nominalizations, marketing adjectives, passive voice, present-perfect forms (including irregular participles such as "has run"), long sentences, synonym rotation, and dangling conjunctions in supported list items. It does not check noun-cluster length (that needs part-of-speech tagging) and it does not know phrasal verbs outside its list, so "take off the panel" passes. It never flags hedges or modality.

The policy reference and worked examples quote patterns they discuss, and some repository prose runs long. The documented baseline command for the entry point remains `python skills/asd-ste100/scripts/ste-lint.py --baseline 40 skills/asd-ste100/SKILL.md`. Read findings in context rather than treating every match as a defect.

The dangling-conjunction rule checks list markers at the start of a line with zero to three leading spaces and ASCII spaces after the marker. It supports unordered markers `-`, `*`, and `+`, and ordered numeric markers that end in `.` or `)`, such as `1.` or `1)`. It checks indented continuation lines up to the final meaningful line. It does not parse list syntax inside blockquotes, lazy continuation, or full nested-list semantics. A standalone line with four or more leading spaces is not treated as a list marker. Within an active list item, indentation at the computed content column is treated as continuation text. Fence detection follows the linter's existing simple rule: a stripped line beginning with three backticks or three tildes toggles the fence state.

The intentionally invalid `skills/asd-ste100/examples/linter-edge-cases.md` file demonstrates incomplete Markdown list items. Run `python skills/asd-ste100/scripts/ste-lint.py skills/asd-ste100/examples/linter-edge-cases.md` to confirm that the linter reports the two expected findings. The file is a test fixture and should not be used as compliant STE prose.

Dictionary scope and redistribution limits: [Source and Scope](skills/asd-ste100/references/writing-rules.md#source-and-scope). Full rules, selected vocabulary evidence, verification guidance, and citations: [`skills/asd-ste100/references/writing-rules.md`](skills/asd-ste100/references/writing-rules.md).

## Installation

### Quick Install (npx skills)

The fastest way to install this skill is the [skills CLI](https://skills.sh/) — no clone, no path setup. Run it from your project root:

```bash
npx skills add danyuchn/asd-ste100-skill
```

This pulls the skill from the GitHub repo and installs it for the current project. The CLI sends anonymous install telemetry (skill name and timestamp, no personal or device information) to help rank skills on the skills.sh leaderboard. Set `DISABLE_TELEMETRY=1` to opt out.

Update later with `npx skills update`.

### Clone

```bash
git clone https://github.com/danyuchn/asd-ste100-skill ~/.claude/skills/asd-ste100-repo
ln -s ~/.claude/skills/asd-ste100-repo/skills/asd-ste100 ~/.claude/skills/asd-ste100
```

This clones the repo and links the skill folder into `~/.claude/skills/`, making the skill available in every Claude Code project. Update later with `git -C ~/.claude/skills/asd-ste100-repo pull`.

## Usage

Trigger with a request to simplify or clarify English text:

```
Disambiguate this tool description
Rewrite this error message so an agent can't misparse it
Apply ASD-STE100 to this instruction
```

Or paste text and ask Claude to "disambiguate this" / "apply STE100 to this" / "reduce ambiguity in this output."

Rewrite requests return the rewritten text alone, except for the permitted `Kept as-is:` note described above. To see which rules were applied, add "show the diff" or "explain the changes" to the request.

Request a review or fixes from existing findings explicitly:

```text
Review this document for ASD-STE100 compatibility
Suggest fixes from these supplied findings without starting a new review
```

These requests use the review table rather than the default rewrite output. Reviews assess readable content, not input-format tooling or extraction validation.

## Scope

Built for: agent-to-agent messages, tool/function descriptions, error messages, system prompts, inter-agent instructions — any English text a machine or non-native reader has to parse without a human to ask.

Not built for: creative writing, marketing copy, or anything where voice and nuance are the point — STE is deliberately flat and literal by design.

One limit worth stating up front: this fixes the form of a text, not its substance. A paragraph with nothing to say comes out short, clean, and still empty.

## Other Languages

- **Hebrew:** [g4lb/asd-ste100-hebrew-skill](https://github.com/g4lb/asd-ste100-hebrew-skill) is a Hebrew port of this skill. It includes a Hebrew linter. ASD-STE100 defines English only, so the Hebrew rules are an adaptation, not an official standard.

## Related Tools

- [meiluosi/rewrite-fidelity-skill](https://github.com/meiluosi/rewrite-fidelity-skill) compares the original text with the rewrite. It flags changes in meaning and modality. It uses pattern matching, so check each flag yourself.

## Sources

- [ASD-STE100 official site](https://www.asd-ste100.org/)
- [ASD-STE100 — About STE](https://www.asd-ste100.org/about_STE.html)
- [ASD Europe — Simplified Technical English](https://www.asd-europe.org/standards-specifications/simplified-technical-english/)
- [Simplified Technical English — Wikipedia](https://en.wikipedia.org/wiki/Simplified_Technical_English)
- [TechScribe — ASD-STE100 Simplified Technical English](https://www.techscribe.co.uk/techw/asd-simplified-technical-english.htm)

## License

MIT — see [LICENSE](LICENSE).
