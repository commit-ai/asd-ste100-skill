# Before / After Examples

## Verification status

These are original, provisional illustrations, not official quotations or fully verified ASD-STE100 Issue 9 text. The full standard and a documented software terminology set were not available for their preparation.

Their [evidence and counting basis](../references/writing-rules.md#evidence-and-verification-limits), [writing policies](../references/writing-rules.md#mode-dependent-enforcement), and [verification procedure](../references/writing-rules.md#completing-strict-ste-verification) are defined in the rule reference.

## Part 1 — Illustrative Rule Applications

The evidence column records the basis and unresolved checks for each transformation.

| Rule | Before | After | Why | Evidence / remaining check |
|---|---|---|---|---|
| Consistent approved wording | "Begin the test before installation. Start the test after installation." | "Start the test before installation. Start the test after installation." | The action and both timings remain; both sentences now use the same verb. | [Selected word-choice restriction](../references/writing-rules.md#word-choice). Other words in these sentences remain unverified. |
| Approved part of speech | "Check the connection." | "Do a check of the connection." | The same action remains, with `check` used as a noun. | [Selected word-choice restriction](../references/writing-rules.md#word-choice). |
| Approved sense, not just plain meaning | "Follow the safety instructions." | "Obey the safety instructions." | This assumes "follow" means "obey" here, rather than physically come after. | A secondary-source illustration of [sense restriction](../references/writing-rules.md#word-choice); the current entries for both words remain unverified. |
| Simple tense where equivalent | "We have received the technical reports from HQ." | "We received the technical reports from HQ." | The after-text treats receipt as a past event. Its equivalence is unresolved if current relevance is essential. | [Verb forms and retained-compound departure](../references/writing-rules.md#verb-forms). |
| Verb, not noun | "Perform an inspection of the filter." | "Inspect the filter." | The after-text expresses the same inspection with a direct verb and adds no task. | [Action-verb preference](../references/writing-rules.md#word-choice). The Issue 9 entry and intended sense of `inspect` remain unverified. |
| Direct wording for an idiomatic action | "Take off the access panel." | "Remove the access panel." | Here, both expressions describe removing the same panel. | A contextual [phrasal-verb candidate](../references/writing-rules.md#phrasal-verbs); the applicable dictionary entries remain unverified. |

## Part 2 — Applied to Agent Output

These cases demonstrate rewrites for another agent, a translation layer, or a non-native reader. Each records source concerns, the proposed text, and remaining choices.

### Example A — Tool description

**Before:**
> This tool will attempt to synchronize state across the various backends that have been configured, and if a conflict is detected it may resolve it automatically depending on the strategy that has been set, or otherwise it will surface the conflict for manual review.

**Concerns identified:**
- Several actions and a fallback in one descriptive sentence, not two commands.
- Compound forms in the relative clauses ("have been configured", "has been set") can become "configured" here.
- 44 words: a [descriptive sentence-length concern](../references/writing-rules.md#sentence-structure).

**Meaning retained:** "Will attempt to" and "may resolve" limit the source's claims. The after-text does not promise success.

**After:**
> The tool will try to synchronize state across the configured backends. If a conflict is detected, the tool may resolve it automatically. This possible resolution depends on the configured strategy. Otherwise, it will report the conflict for manual review.

The attempt and possible resolution remain uncertain. No strategy-reading operation is added.

**Unresolved author choice:** "Otherwise" could cover every unresolved conflict or only a strategy that excludes automatic resolution. The rewrite leaves those alternatives unsettled.

**Remaining checks:** Word senses, software terms, and verb forms remain unverified. The passive detection clause retains the source's unspecified actor; its [voice assessment](../references/writing-rules.md#voice) depends on that context.

### Example B — Error message

**Before:**
> An error may have occurred while processing your request due to a possible mismatch in the expected data format, which could be caused by an outdated client version.

**Concerns identified:**
- One sentence carrying three uncertain claims (a possible error, a possible format mismatch, a possible outdated-client cause).
- 28 words: a [descriptive sentence-length concern](../references/writing-rules.md#sentence-structure).

**Meaning retained:** The possible error and both possible causes remain uncertain.

**After:**
> An error may have occurred while processing your request. A mismatch with the expected data format may be the cause. An outdated client version could cause this mismatch.

An error is not necessarily a failed request. The rewrite preserves the processing context and both uncertain causal links. It adds no server, frequency claim, or troubleshooting instruction.

**Retained departure:** "May have occurred" retains the uncertain past event through the [local compound-form departure](../references/writing-rules.md#verb-forms). "While processing" also remains an `-ing` verb construction. Grammatical and dictionary checks remain unresolved, and the source supplies no processing actor.

### Example C — Inter-agent instruction

**Before:**
> Once the upstream job has completed and assuming no errors were raised, the downstream agent should proceed to consume the output artifact, though it is worth noting that partial artifacts are sometimes produced under timeout conditions.

**Concerns identified:**
- Subordinate-clause stacking ("assuming...", "though it is worth noting...").
- Present perfect ("has completed") and passive clauses are grammatical review candidates; the completion condition is substantive.
- One sentence, three separate facts (completion condition, next action, edge-case warning).
- 36 words: an [instruction sentence-length concern](../references/writing-rules.md#sentence-structure).

**After:**
> After the upstream job completes, if no errors were raised, the downstream agent should consume the output artifact. Partial artifacts are sometimes produced under timeout conditions.

The recommendation remains `should`, not a mandatory command. Both prerequisites now precede the downstream action, consistent with the [work-step condition guidance](../references/writing-rules.md#sentence-structure). "After ... completes" retains the completion prerequisite without present perfect. The occasional partial-artifact warning remains descriptive. No waiting or completeness-checking instruction is added.

**Remaining checks:** The output is still a recommendation rather than an imperative procedure. Passive clauses, `should`, and software terms remain unverified. The source identifies neither the error-reporting actor nor the artifact-producing actor; those are specific missing author inputs for any recast that names them.

### Example D — README prose (STE-flavored mode)

**Request:** "Apply ASD-STE100 to this README paragraph." This explicit request admits the explanatory prose; a generic request to make it clearer would not.

**Before:**
> Our caching layer is designed to slot seamlessly into your existing stack with minimal friction and no vendor lock-in; it leverages semantic similarity to dramatically reduce the cache misses that traditionally plague LLM workloads.

**Concerns identified:**
- Marketing adjectives and claims without measurement ("seamlessly", "minimal friction", "dramatically").
- Semicolon joining two separate ideas.
- Idiomatic and soft phrasing ("slot ... into", "leverages"). The design status itself is meaningful, not disposable framing.
- 34 words: a [descriptive sentence-length concern](../references/writing-rules.md#sentence-structure).

**After:**
> Our caching layer is designed to integrate easily with your existing stack without vendor lock-in. It uses semantic similarity with the aim of greatly reducing the cache misses that LLM workloads traditionally experience.

The rewrite preserves design intent, semantic similarity, and the lock-in claim. It adds no exact-text cache comparison, runtime integration guarantee, or data-location claim.

**Unresolved author choice:** "Easily", "greatly", and "traditionally" retain the source's unmeasured benefit claims. The effort criterion and evidence for the reduction and recurring misses were not supplied. Quantifying those claims or obtaining permission to remove them remains unresolved.

**Remaining checks:** Workloads that "experience" misses is a figurative construction. Its word senses, the verb forms, and the technical terms remain unverified.

## Part 3 — Contextual Review Examples

These cases demonstrate the [review report contract](../references/review-workflow.md#report-contract).

### Literal versus idiomatic use

"Go to the next page." describes literal navigation and needs no edit on idiom grounds.

"People other staff go to for technical help." describes help-seeking. Direct wording may be clearer, but the lexical concern is not a proven dictionary violation.

### Borderline versus confirmed findings

| Location | Source expression | Status | Reason / basis | Suggested edit or author decision |
|---|---|---|---|---|
| Part 3, Literal versus idiomatic use | "People other staff go to for technical help." | Borderline | "Go to" describes help-seeking here. Whether a lexical change is required remains unverified. | If help-seeking is intended: "People whom other staff ask for technical help." |
| Example D, Before | "no vendor lock-in; it leverages semantic similarity" | Confirmed | The quoted semicolon is a [Rule 8.1 conflict](../references/writing-rules.md#sentence-structure). The benefit claims remain unverified. | Example D's provisional two-sentence rewrite retains the design and semantic-similarity claims. |
