---
name: asd-ste100
description: "Review documents for ASD-STE100 compatibility, suggest fixes from supplied findings, or rewrite English that is dense or easy to misparse. Use for tool descriptions, error messages, inter-agent instructions, system prompts, and status reports where misreading has a real cost. Triggers: STE100 review, disambiguate, apply Simplified Technical English, plain-language rewrite, controlled-language rewrite, rewrite so an agent cannot misread this. Not for creative or marketing copy."
version: 0.4.0
---

# Simplified Technical English (ASD-STE100)

ASD-STE100 is a controlled-language standard built by the aerospace and defense industry (ASD, the AeroSpace and Defense Industries Association of Europe) to stop maintenance technicians from misreading English instructions. The standard removes the two biggest sources of misreading: words with more than one meaning, and sentences with more than one possible structure.

This skill borrows that same discipline for a different reader: an **AI agent or a downstream system** that has to parse an English string — an error message, a tool description, an inter-agent instruction, a status report — without a human in the loop to resolve ambiguity. If a maintenance technician can misread "close the valve" as an adjective ("the valve that is near") instead of a command, so can a language model.

## When to Use This Skill

- An agent's output (explanation, instruction, log message, tool description) reads as dense, jargon-heavy, or ambiguous.
- Text will be consumed by another agent, a translation pipeline, or a non-native English reader, and misparsing has a real cost.
- You are writing a prompt, system message, or tool description and want to remove ambiguity before a model ever sees it.
- You want a **before/after** comparison showing exactly which rule was violated and how the rewrite fixes it. Ask for it — the default output is the rewritten text alone (see Output Format).

This skill is not for creative or marketing copy — STE is deliberately flat and literal. Do not apply it to text where voice, nuance, or persuasion is the point.

## Task Routing

- **Document review or compatibility assessment:** Read [references/review-workflow.md](references/review-workflow.md) and follow its review workflow and report contract.
- **Suggested fixes from supplied findings:** Read the same reference and follow its supplied-fixes branch. Use only the supplied findings.
- **Rewriting:** Follow the Process and Output Format below. Keep ordinary task inference and the plain-text rewrite default.

Strict and STE-flavored are writing policies for these tasks, not additional task types.

## Two Modes

Pick a mode before rewriting. If the user does not say which, infer it from the text type. Keep the choice internal unless the user asks for the rule table (see Output Format).

**Strict** — procedures, error messages, tool and function descriptions, inter-agent instructions, safety text. Anywhere a wrong reading has a cost. Apply every rule below, including the hard length caps and one-word-one-meaning discipline.

**STE-flavored** — READMEs, PR descriptions, changelogs, explanatory prose. Apply the structural rules in full and treat the lexical rules as advisory (see Core Rewrite Rules for that split). In practice that means keeping the sentence length caps, active voice, simple tenses, no phrasal verbs, no semicolons, no nominalization and no marketing adjectives, while dropping the one-word-one-meaning lockdown: prose needs some range, and a strict rewrite of prose reads as a personality transplant rather than a clarification.

The two modes and the structural/lexical split are the same distinction seen from two directions. The split says which rules this skill can verify without ASD's dictionary. The modes say which of them to enforce for a given kind of text.

These are local writing policies, not ASD conformance levels. Strict mode does not certify compliance. If source fidelity requires a retained departure, identify it as a departure rather than an exception permitted by ASD-STE100. See the [bundled guidance and verification limits](references/writing-rules.md#evidence-and-verification-limits).

## Source and Scope

This skill encodes the **rule categories** of ASD-STE100 Issue 9 (Jan 2025): 53 writing rules across 9 sections covering word choice, grammar, sentence structure, and style, backed by a dictionary of ~900 approved words with restricted meanings and parts of speech, and ~1,200 words to avoid with suggested replacements. See `references/writing-rules.md` for the rule summary and citations.

It does **not** reproduce ASD's ~900-word approved dictionary verbatim. ASD-STE100 is free to obtain, but it is not free to redistribute: Issue 9, page 2 states that "no reproduction or publication of it, in whole or in part, shall be made without the written authority of an officer of ASD," and grants free reproduction rights only to eight listed categories (ASD/AIA/AIAC member associations and their member companies and customers, member-state defence ministries, A4A, airworthiness authorities, and universities and research institutes for educational purposes). This project is in none of them, so the dictionary stays out of this repo.

Use the bundled verified word restrictions where applicable. For other words, prefer plain and consistent wording without claiming dictionary approval. When exact ASD-approved wording matters (e.g. actual aircraft maintenance documentation), get the standard and check word-by-word against the real dictionary. Request it from the [official downloads page](https://www.asd-ste100.org/STE_downloads.html) — note that this is a request form that emails you a link, not a direct download.

## Core Rewrite Rules

**Structural rules** describe sentence and document shape. **Lexical rules** restrict word meanings and parts of speech. The bundled rule reference includes selected verified vocabulary facts, not the complete official dictionary (see Source and Scope). Use those facts where applicable. Plain wording alone does not prove approval of other words or senses.

Apply the structural rules in context. Use the selected verified restrictions as lexical evidence; other plain-language preferences do not prove dictionary compliance. Explain that limitation in reviews or requested reasoning, without adding commentary to default rewrites.

### Structural rules — apply these

| Rule | Do | Don't |
|---|---|---|
| Active voice | "The agent deletes the file." Use direct imperatives for procedures. | Passive procedures, or descriptive passives with a known actor. Descriptive passives are permitted when the actor is unknown, not merely irrelevant. |
| No phrasal verbs (Rule 9.3) | "Remove the panel." / "Start the job." | "Take off the panel." / "Spin up the job." — a two-word verb has meanings the parts do not predict |
| One instruction per sentence | "Open the file. Read line 3." | "Open the file and read line 3, then check if it matches." |
| Prerequisites before actions | State a condition before a work-step action if the reader needs it before acting | Put a required condition after the action, or invent a missing condition |
| Sentence length | ≤20 words for instructions/procedures, ≤25 words for descriptions | Long compound/subordinate-clause sentences |
| No semicolons (Rule 8.1) | Split into separate sentences | Any semicolon at all — STE bans the mark outright, not only as a clause join. (Rule 8.1 permits every other standard punctuation mark. The em dash is *not* banned by STE, though it often signals a sentence that should be split.) |
| Noun clusters | ≤3 words stacked as a noun phrase ("fuel pump valve") | 4+ word noun stacks ("high pressure fuel pump inlet valve assembly") |
| No ellipsis | Keep the subject, verb, and article explicit even if it reads longer | Drop words to save space ("Files not backed up will be lost" → ambiguous which files) |
| Keep modality | "The request **may have** failed." stays "may have" | Promote a hedge to a fact ("The request failed.") or invent a certainty the source did not state |
| Paragraph limits | One topic per paragraph, ≤6 sentences | Multi-topic paragraphs |
| Lists for sequences | Use a numbered or bulleted list for 3+ steps or conditions | Bury a sequence inside one prose sentence |

### Lexical rules — selected facts and dictionary-dependent guidance

| Rule | Do | Don't | Why it is weaker here |
|---|---|---|---|
| Approved meaning | Use one approved term consistently for the same action, such as "start" rather than "begin" | Rotate synonyms for the same idea, or use an unapproved sense of an otherwise approved word | Consistency and approval are separate checks. Use the [selected restrictions](references/writing-rules.md#word-choice); verify other entries rather than inferring approval. |
| Approved part of speech | "Do a check of the connection" (check = noun) | "Check the connection" (check = verb) | Noun `check` is approved; verb `check` is not. Do not generalize this fact to unverified words. |
| Verb, not noun (Rule 3.7) | Prefer a direct **approved** action verb where equivalent | Convert an approved noun into an unapproved verb merely to make the sentence shorter | Approval and meaning take priority over the verb preference. A nominalization match alone does not justify a substitution. |
| Domain terms | Keep necessary technical nouns/verbs, define unfamiliar ones, and establish their documented basis | Use undefined jargon, or declare a word technical solely to bypass a restriction | Apply the [technical-terminology criteria](references/writing-rules.md#technical-terminology). A definition alone does not establish approval. |

### Simple tenses and the skill's fidelity exception

STE restricts verb forms, including infinitive, imperative, simple present, simple past, simple future, and past participles as adjectives. Limited descriptive passives are also permitted. Present perfect is excluded: "we received the report", not "we have received the report", when equivalent. Verify permitted constructions against the complete standard rather than treating every auxiliary as forbidden.

The tense restriction and this skill's fidelity policy are separate. **Where a compound form carries necessary information that a supported rewrite cannot preserve, keep it and flag the departure.** A hedge such as "may have failed" must not become a definite failure. This is a local fidelity exception, not an exception granted by ASD-STE100. First consider an equivalent simple form. For example, "after the job completes" can preserve a completion prerequisite without "has completed".

## Scan Checklist

Scan for these six habits before rewriting. Punctuation and word counts are observable checks. Synonym equivalence, idiomatic meaning, and rule applicability require contextual judgment. A regex match alone proves neither a violation nor dictionary approval.

1. **Synonym rotation** — the same thing gets several names in one document ("the user", "the customer", "the client"). First establish that the names refer to the same thing. Then use one name consistently. Preserve distinct actions, objects, and parts of speech.
2. **Hedge stacking** — helper verbs and qualifiers obscure the claim ("it is important to note that this may potentially help to improve"). Remove empty framing while preserving uncertainty and the claim's scope.
3. **Nominalization** — an action expressed through a noun ("perform an analysis of", "provides assistance to"). Prefer an equivalent approved verb. Preserve a noun when its corresponding verb is not approved.
4. **Marketing adjectives** — words that claim quality instead of showing it: seamless, robust, powerful, cutting-edge, effortless, blazing-fast. Remove empty praise. Retain substantive design or benefit claims as claims, and request evidence when needed. Use measurements only if supplied.
5. **Run-on sentences** — several ideas joined by semicolons or em dashes. Fix: one idea per sentence.
6. **Soft phrasal verbs** — spin up, reach out, dive into, kick off. Use an equivalent approved verb where possible, such as "start" rather than "begin".

## Process

This is the rewrite path. Review and supplied-fixes tasks use the reference selected in Task Routing.

1. Pick the mode (Strict or STE-flavored). Say which only when the user asked for the rule table — see Output Format.
2. Read the input text once for meaning — do not start rewriting before you understand what it must still say afterward.
3. Walk it sentence by sentence. Flag every rule violation from the Core Rewrite Rules tables and every habit from the Scan Checklist. In STE-flavored mode, flag the lexical rules but do not enforce them. For a mechanical first pass over the structural rules, run `scripts/ste-lint.py` (stdin or file args, `--json` for structured output); it checks semicolons, sentence length, phrasal verbs, nominalization, marketing adjectives, synonym rotation, dangling-conjunction in supported list items, passive voice, and compound tenses, and by design never flags hedges or modality. `--baseline N` tolerates N hard violations (for adopting on existing docs); `--disable rule1,rule2` silences named rules.
   - For word-approval questions, technical terminology, or grammatical edge cases, read the [bundled rule reference](references/writing-rules.md). Apply its known restrictions locally; leave other dictionary-dependent judgments unverified.
4. Rewrite each flagged sentence to fix the violation while preserving the original meaning exactly. If a rewrite would drop necessary precision (a safety condition, a scope qualifier, a number), keep the longer phrasing and flag it instead of silently simplifying.
   - **Check modality before you commit to a rewrite.** Hedges ("may", "could", "sometimes", "is likely to") carry the author's confidence, and confidence is content. A shorter sentence that upgrades a hedge to a fact is not a simplification — it is a different claim. This is the most common way a well-intentioned STE rewrite goes wrong, because hedges are exactly what a length cap tempts you to cut.
   - Never add a fact the source did not state. A rewrite that reads better because it supplies a cause, a frequency, or a mechanism has stopped being a rewrite.
5. Output the rewritten text (see Output Format). Keep the mode choice and the rule analysis internal unless the user asked to see them.
6. If the input already complies, say so — do not force changes onto compliant text.

## Output Format

**Default: the rewritten text, and nothing else.** Most callers want a result they can paste straight into a tool description, an error string, or a prompt. Print the simplified text on its own. Do not add a preamble about this skill, a mode announcement, a violation count, a summary of what changed, a rule table, or a closing offer to explain further.

The one permitted addition: if step 4 kept a longer phrasing on purpose, add a single line after the text, prefixed `Kept as-is:`, naming the phrase and the precision that would have been lost. Omit the line when there is nothing to report.

**On request: the rule table.** When the user asks to see the reasoning — "show the diff", "which rules did it break", "explain the changes", "before/after" — output this table instead:

```markdown
| Rule violated | Original | Simplified |
|---|---|---|
| Present perfect tense | "We have received your request." | "We received your request." |
| Noun cluster (4+ words) | "the agent task queue priority handler" | "the handler that sets task-queue priority" |

Mode: Strict. 7 violations found.
```

Follow the table with a one-line note on anything you deliberately did **not** simplify, and why (usually: simplifying would lose required precision).

## Boundaries

**Will:**
- Rewrite ambiguous or dense English into short, single-meaning, active-voice sentences.
- Return the rewritten text alone by default, and name the rules it applied when the user asks.
- Preserve every fact, condition, and scope qualifier in the original.
- Preserve the strength of every hedge, and add no claim the source did not make.
- Suggest a one-line glossary entry for domain terms that must stay.

**Will not:**
- Reproduce ASD's official ~900-word dictionary as if it were memorized verbatim — always treat the official download as the source of truth for exact approved wording.
- Simplify creative, marketing, or persuasive copy where voice and nuance are the point.
- Silently drop a safety condition, exception, or scope qualifier to shorten a sentence — it will flag the trade-off instead.
- Convert "may have failed" into "failed", or "could be caused by X" into "X is the cause" — losing a hedge changes the claim.
- Guarantee an aerospace/defense-grade STE-compliant document. This is a general-purpose clarity tool inspired by STE, not a certified STE authoring tool.
- Make weak content true or useful. STE fixes the *form* of a text, not its substance. A hollow paragraph rewritten under these rules becomes a clean, short, well-punctuated hollow paragraph. If the text has nothing to say, no rewrite fixes that — say so instead of polishing it.
- Shorten past the point of clarity. Cutting words is not the goal. Removing ambiguity is the goal. Past a certain point compression starts costing the reader time rather than saving it, so stop when the sentence is unambiguous, not when it is shortest.

## Additional Resources

- **`references/writing-rules.md`** — fuller summary of the 9 rule sections and dictionary structure, with citations to the official standard and secondary sources.
- **`examples/before-after.md`** — illustrative rule applications, agent-output rewrites, and contextual review examples.
- **`scripts/ste-lint.py`** — deterministic, stdlib-only linter for the structural rules, including dangling-conjunction in supported list items, plus a synonym-rotation check (one word, one meaning) scoped per file. Exit 1 when hard violations exceed `--baseline` (default 0); advisory findings (passive voice, compound tenses) never fail the run; `--disable` silences named rules. It never flags hedges or modality: those are content, not style, and `--selftest` asserts that "may have failed" passes clean.
