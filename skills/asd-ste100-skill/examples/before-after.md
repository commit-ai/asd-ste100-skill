# Before / After Examples

## Verification status

These examples are not fully verified ASD-STE100 Issue 9 text. The [bundled rule reference](../references/writing-rules.md) contains the selected verified restrictions used below. It does not replace the complete standard or a word-by-word dictionary review. The full standard and a documented software terminology set were not available for this review.

Part 1 illustrates individual rule categories, not whole-sentence approval. Parts 2 and 3 demonstrate this skill's fidelity and review policies. A retained departure or unresolved author decision is not an STE-compliant result. In particular, this skill's Strict and STE-flavored modes are local policies, not ASD conformance levels.

## Part 1 — Illustrative Rule Applications

These are illustrations, not official examples or quotations from the standard. The evidence column identifies known restrictions and remaining verification work. An approved word alone does not establish approval of every word or construction in a sentence.

| Rule | Before | After | Why | Evidence / remaining check |
|---|---|---|---|---|
| Consistent approved wording | "Begin the test before installation. Start the test after installation." | "Start the test before installation. Start the test after installation." | Retain the action and both timings while using the selected synonym. | The [word-choice restrictions](../references/writing-rules.md#word-choice) select `start`, not `begin`. Other words in these sentences still require dictionary review. |
| Approved part of speech | "Check the connection." | "Do a check of the connection." | Retain the check as an action, but use `check` as a noun. | The word-choice restrictions approve noun `check`, not verb `check`. This is not a reason to rename all distinct checking or verification actions. |
| Approved sense, not just plain meaning | "Follow the safety instructions." | "Obey the safety instructions." | This assumes "follow" means "obey" here, rather than physically come after. | A secondary-source illustration of sense restriction, not a verified current dictionary entry. Verify both entries before claiming compliance. |
| Simple tense where equivalent | "We have received the technical reports from HQ." | "We received the technical reports from HQ." | Use this only if a past event is all the source needs to report. If current relevance is essential, report the unresolved fidelity issue rather than claim this substitution is equivalent. | Apply the [verb-form guidance](../references/writing-rules.md#verb-forms). This skill's permission to retain a necessary compound form is a departure, not an exception granted by the standard. |
| Verb, not noun | "Perform an inspection of the filter." | "Inspect the filter." | Make the action direct without adding another task. | This illustrates the skill's action-verb preference. Verify `inspect` and its intended meaning in the Issue 9 dictionary before calling the sentence STE-compliant. |
| Direct wording for an idiomatic action | "Take off the access panel." | "Remove the access panel." | Here, both expressions describe removing the same panel. Multiple dictionary senses alone do not prove that this occurrence is ambiguous. | This is a contextual rewrite candidate. Verify the applicable rule and dictionary entries in Issue 9 before asserting full compliance. |

## Part 2 — Applied to Agent Output

These are original examples built for this skill's actual use case: rewriting AI agent output for another agent, a translation layer, or a non-native reader. They are provisional clarity rewrites, not approved STE models. The source's meaning takes priority over inventing a compliant-looking replacement.

Counts below use whitespace-separated tokens (`text.split()`), with punctuation not counted separately. They are sanity checks, not verified counts under the standard's counting rules. Short sentences alone do not establish compliance.

### Example A — Tool description

**Before:**
> This tool will attempt to synchronize state across the various backends that have been configured, and if a conflict is detected it may resolve it automatically depending on the strategy that has been set, or otherwise it will surface the conflict for manual review.

**Concerns identified:**
- Several actions and a fallback in one descriptive sentence, not two commands.
- Compound forms in the relative clauses ("have been configured", "has been set") can become "configured" here.
- 44 words, far over the 25-word descriptive cap.

**Fidelity constraints:** "Will attempt to" and "may resolve" limit the source's claims. The rewrite must not promise success. Preserving these qualifications does not establish that their verb forms or word choices are approved.

**After:**
> The tool will try to synchronize state across the configured backends. If a conflict is detected, the tool may resolve it automatically. This possible resolution depends on the configured strategy. Otherwise, it will report the conflict for manual review.

The attempt and possible resolution remain uncertain. No strategy-reading operation is added. "Otherwise" retains an ambiguity from the source: does the fallback cover every unresolved conflict, or only a strategy that excludes automatic resolution? Ask the author to choose before making that condition explicit. This rewrite does not settle that policy question.

**Not ready for strict-STE approval:** The fallback needs an author decision. Word senses, software technical terms, and permitted verb forms still need Issue 9 review. The passive detection clause does not supply an actor the source never identified. The [voice guidance](../references/writing-rules.md#voice) permits passive voice in descriptive text only when the actor is unknown.

### Example B — Error message

**Before:**
> An error may have occurred while processing your request due to a possible mismatch in the expected data format, which could be caused by an outdated client version.

**Concerns identified:**
- One sentence carrying three uncertain claims (a possible error, a possible format mismatch, a possible outdated-client cause).
- 28 words, over the descriptive cap.

**Fidelity constraints:** "May have occurred" and "could be caused by" preserve the source's uncertainty. Do not remove that uncertainty merely to satisfy a tense preference. This does not make those constructions STE-approved.

**After:**
> An error may have occurred while processing your request. A mismatch with the expected data format may be the cause. An outdated client version could cause this mismatch.

An error is not necessarily a failed request. The rewrite preserves the processing context and both uncertain causal links. It adds no server, frequency claim, or troubleshooting instruction. A rewrite that supplies a cause, frequency, or mechanism has stopped being a rewrite.

**Retained departure:** "May have occurred" keeps a compound verb form under this skill's fidelity policy, not an exception established in ASD-STE100. "While processing" also remains an `-ing` verb construction. The [verb-form guidance](../references/writing-rules.md#verb-forms) generally excludes `-ing` verbs while permitting specified non-verb uses, such as technical nouns. This output needs further grammatical and dictionary work before strict-STE approval. Recasting it must preserve the uncertain past event and supply no new processing actor.

### Example C — Inter-agent instruction

**Before:**
> Once the upstream job has completed and assuming no errors were raised, the downstream agent should proceed to consume the output artifact, though it is worth noting that partial artifacts are sometimes produced under timeout conditions.

**Concerns identified:**
- Subordinate-clause stacking ("assuming...", "though it is worth noting...").
- Present perfect ("has completed") and passive clauses require grammatical review. Preserve the completion condition when changing the tense.
- One sentence, three separate facts (completion condition, next action, edge-case warning).
- 36 words, over the 20-word instruction cap.

**After:**
> After the upstream job completes, if no errors were raised, the downstream agent should consume the output artifact. Partial artifacts are sometimes produced under timeout conditions.

The recommendation remains `should`, not a mandatory command. Both prerequisites now precede the downstream action, consistent with the [work-step condition guidance](../references/writing-rules.md#sentence-structure). "After ... completes" retains the completion prerequisite without present perfect. The occasional partial-artifact warning remains descriptive. No waiting or completeness-checking instruction is added.

**Not ready for strict-STE approval:** A recommendation about an agent is not an imperative procedure. The output retains passive clauses and `should`; these need review against the applicable procedural/descriptive rules and dictionary. If a compliant rewrite requires an error-reporting or artifact-producing actor, ask the author rather than invent one. Software terms also need documented terminology evidence.

### Example D — README prose (STE-flavored mode)

**Before:**
> Our caching layer is designed to slot seamlessly into your existing stack with minimal friction and no vendor lock-in; it leverages semantic similarity to dramatically reduce the cache misses that traditionally plague LLM workloads.

**Concerns identified:**
- Marketing adjectives and claims without measurement ("seamlessly", "minimal friction", "dramatically").
- Semicolon joining two separate ideas.
- Idiomatic and soft phrasing ("slot ... into", "leverages"). The design status itself is meaningful, not disposable framing.
- 34 words, over the 25-word descriptive cap.

**After:**
> Our caching layer is designed to integrate easily with your existing stack without vendor lock-in. It uses semantic similarity with the aim of greatly reducing the cache misses that LLM workloads traditionally experience.

The rewrite preserves design intent, semantic similarity, and the lock-in claim. It adds no exact-text cache comparison, runtime integration guarantee, or data-location claim.

**Unresolved author decision:** "Easily", "greatly", and "traditionally" retain the source's unmeasured benefit claims. Ask for the effort criterion and evidence for the reduction and recurring misses. Replace these claims with supplied evidence, or obtain permission to remove them. This is a faithful provisional rewrite, not a claim that those concerns are resolved.

**Not ready for strict-STE approval:** STE-flavored is a local adaptation. Figurative uses such as workloads that "experience" misses, verb forms, word senses, and technical terms still need review. A shorter marketing claim is neither verified evidence nor proof of STE compliance.

## Part 3 — Contextual Review Examples

These pairs illustrate review judgments, not a phrase blacklist. Use the [review workflow](../references/review-workflow.md) for the report contract. Neither their proposed edits nor all their words have been approved against the Issue 9 dictionary.

### Literal versus idiomatic use

"Go to the next page." describes literal navigation and needs no edit on idiom grounds.

"People other staff go to for technical help." describes help-seeking. Direct wording may be clearer, but the lexical concern is not a proven dictionary violation.

### Borderline versus confirmed findings

| Location | Source expression | Status | Reason / basis | Suggested edit or author decision |
|---|---|---|---|---|
| Part 3, Literal versus idiomatic use | "People other staff go to for technical help." | Borderline | "Go to" describes help-seeking here. Whether a lexical change is required remains unverified. | If help-seeking is intended: "People whom other staff ask for technical help." |
| Example D, Before | "no vendor lock-in; it leverages semantic similarity" | Confirmed | The semicolon conflicts with the punctuation rule (Rule 8.1). This does not prove the benefit claims. | Split the clauses into sentences while preserving the design and semantic-similarity claims, as in the provisional rewrite. |

## How to Read These Examples

Part 1 illustrates rule categories with context-dependent lexical choices. Part 2 applies the discipline to agent output while preserving meaning. Part 3 separates supported findings from unresolved contextual concerns. Deterministic checks can identify punctuation and length patterns, but they cannot prove semantic equivalence, lexical approval, or complete review coverage.

## Completing strict-STE verification

Use the [official Issue 9 request route](https://www.asd-ste100.org/STE_downloads.html#article02-2l) to obtain the standard. Check each proposed sentence against the full writing rules and each general word against its permitted meaning and part of speech. Check technical nouns and verbs against applicable documented terminology, rather than declaring arbitrary words technical to bypass the dictionary.

Resolve the author decisions above, apply the standard's word-counting rules, and have an STE-competent editor review grammar, technical meaning, and source fidelity together. [STEMG training guidance](https://www.asd-ste100.org/STE_training.html) identifies the standard as the indispensable reference. [STE support teams](https://www.asd-ste100.org/STEWorkingGroups.html) and [STEMG trainers](https://www.asd-ste100.org/STEtrainers.html) are legitimate consultation routes. Until those checks are complete, keep the outputs provisional.
