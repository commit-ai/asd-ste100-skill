# ASD-STE100 Writing Policy — Rules and Sources

This reference defines the skill's language rules, source-fidelity constraints, and verification policy. It paraphrases ASD-STE100 rule categories and includes selected verified restrictions.

## Evidence and verification limits

Use the guidance below directly. It includes selected verified vocabulary restrictions, grammatical distinctions, and application limits, so applying those points does not require retrieving a web page.

This is not the complete Issue 9 standard or dictionary. The selected facts support only the restrictions stated, not approval of whole sentences. Other entries, rule numbers, exceptions, and the standard's word-counting method still require the full current standard. For uncovered words, prefer plain, consistent wording while leaving approval or prohibition unverified. Never invent a dictionary entry or claim certified compliance.

Punctuation and local word counts are observable checks. Synonym equivalence, idiomatic meaning, and rule applicability require contextual judgment. A plain word, several possible dictionary senses, or a regex match alone proves neither a violation nor approval. Example counts use whitespace-separated tokens (`text.split()`), with punctuation not counted separately. These are sanity checks, not verified counts under the standard.

Checking tools are optional. Lint findings are candidates, not conclusions. Clean lint proves neither source fidelity nor complete review coverage. Neither a tool result nor an AI opinion replaces the standard or an informed content review. ASD and the STEMG do not endorse or certify checker vendors.

## Mode-dependent enforcement

The [entry point](../SKILL.md#mode-selection) selects the mode. Strict applies every applicable rule below. STE-flavored applies structural rules in full and flags lexical concerns without enforcing them.

Structural rules cover phrasal verbs, verb forms, voice, sentence and paragraph shape, and safety-instruction structure. Lexical rules cover approved meanings and parts of speech, the approved-action-verb preference, and technical terminology. The framing and claim criteria also apply to prose; its original mode guidance includes no nominalization and no marketing adjectives.

These modes are local writing policies, not ASD conformance levels. Their enforcement remains subject to the evidence limits above. The retained-compound-form departure is defined under [Verb forms](#verb-forms).

## Source and Scope

ASD-STE100 is a controlled natural language, first released in 1986 (as AECMA Document PSC-85-16598) by what is now ASD (the AeroSpace and Defense Industries Association of Europe). It was built at the request of European airlines — most staffed by non-native English speakers — who needed maintenance documentation that could not be misread, because a misread instruction on an aircraft can kill people. The standard is maintained by the Simplified Technical English Maintenance Group (STEMG) and has been free to download since Issue 6 (2013). The current edition is Issue 9 (January 2025).

The standard contains:

- **53 writing rules across 9 sections** covering word choice, grammar, sentence structure, and style.
- **A dictionary** of roughly 900 approved words with restricted meanings and parts of speech, plus roughly 1,200 words to avoid with suggested replacements. Usually a word has one approved meaning and one approved part of speech; verify the actual entry rather than treating this as an exception-free rule.
- **A terminology allowance**: organizations may define their own dictionary of approved technical nouns and verbs beyond the base ~900 words, for domain-specific vocabulary the base dictionary can't cover.

The official dictionary stays outside this repository. Issue 9, page 2 restricts reproduction to ASD's written authorization or eight listed categories of organizations: ASD/AIA/AIAC member associations, their member companies and customers, member-state defence ministries, A4A, airworthiness authorities, and universities and research institutes for educational purposes. This project is in none of those categories. Free availability does not grant unrestricted redistribution rights.

## Rule Categories (Paraphrased)

### Word choice

- Use approved words only in their approved meaning and part of speech.
- Do not use another ordinary-English sense of a word merely because context makes it understandable.
- Choose the approved synonym, not just the one that seems plainest. Simplicity and frequency informed the vocabulary selection, but do not independently establish approval.
- For the same action or object, use one term consistently after establishing equivalence. Preserve distinct actions, objects, and parts of speech. For example, noun `checks` and verb `verify` need not name the same action.
- **Nominalization (Rule 3.7):** prefer an equivalent approved action verb over a noun construction such as "perform an analysis of" or "provides assistance to". Approval and meaning take priority over brevity. A nominalization match alone does not justify a substitution.

Selected verified restrictions:

| Word | Apply this restriction |
|---|---|
| `start` | Use this selected verb instead of rotating among synonyms such as `begin`, `commence`, or `initiate`. |
| `check` | Approved as a noun, not as a verb. A construction such as "Do a check" uses the noun. Preserve the approved noun rather than converting it to an unapproved verb for a shorter action sentence. |
| `fall` | The approved verb sense concerns gravity-driven downward movement, not a decrease in a quantity. |
| `about` | The approved sense concerns a topic, not numerical approximation. For an approximation, `approximately` or `around` can be approved alternatives when their intended sense fits. |

Approved meanings and spelling follow American English conventions based on Merriam-Webster. An ordinary dictionary can explain English, but it does not decide STE approval. Restrictions not covered here require the corresponding STE entry.

### Technical terminology

Technical nouns and technical verbs extend the controlled general vocabulary for a company, industry, or subject field. Establish their use from applicable documentation, engineering drawings, company glossaries, or terminology databases and the standard's subject-field categories.

A technical term can contain a word that is not approved independently in the general dictionary. This does not authorize that word outside the term, or make arbitrary jargon a technical term. Keep this use limited. A definition improves readability but is not, by itself, evidence of approved technical-term status.

Verify the term's intended meaning and use consistently. If its expansion, definition, or documented basis is missing, report that specific gap rather than inventing one.

Suggest a one-line glossary entry for a domain term that must stay, and define unfamiliar terms. This improves readability; it does not establish their documented basis.

### Phrasal verbs

Do not make phrasal verbs by putting a verb and a preposition together (Rule 9.3). Their idiomatic meaning is not predictable from the parts. Use an equivalent approved verb where possible: "Remove the panel" rather than "Take off the panel", or "Start the job" rather than "Spin up the job".

Scan for soft phrasal verbs such as spin up, reach out, dive into, kick off, circle back, and touch base. Distinguish literal navigation from idiomatic help-seeking when assessing "go to"; a phrase is not a context-free blacklist entry.

### Verb forms

- Permitted forms include infinitive, imperative, simple present, simple past, simple future, and past participles as adjectives. Limited descriptive passive constructions also use past participles. Verify the permitted constructions against the complete standard.
- The secondary tense summary excludes present perfect: "We have received" becomes "We received" only when the meaning is equivalent. This is not a blanket prohibition of every auxiliary: simple future and permitted descriptive passives also need their applicable rules.
- Generally exclude "-ing" verb forms. Permitted uses include technical nouns or parts of technical nouns, and dictionary-approved nouns, adjectives, pronouns, or prepositions. For example, `opening` can be a noun and `remaining` an adjective; an ending alone does not identify a violation. Verify the actual part of speech and permitted sense.

First consider an equivalent simple form. For example, "after the job completes" can preserve a completion prerequisite without "has completed". Where a compound form carries necessary information that a supported rewrite cannot preserve, keep it and flag the departure. This is the skill's local fidelity exception, not an exception granted by ASD-STE100.

### Source fidelity

Preserve every fact, actor, action, object, alternative, selection count, example, number, timing, condition, exception, scope qualifier, and human approval. Keep documentation and applicability claims separate from claims about actual practice. Keep recommendations as recommendations, design intentions as intentions, and permission as permission.

Preserve the strength of uncertainty, including "may", "could", "sometimes", and "is likely to". Confidence is content: "may have failed" must not become "failed", and "could be caused by X" must not become "X is the cause".

Add no fact the source did not state, including causes, frequencies, mechanisms, architecture, actors, or troubleshooting instructions. If an equivalent edit is unsupported, retain the precision and identify the unresolved issue. Keep necessary longer phrasing and flag the trade-off rather than silently dropping content to meet a length cap.

Stop when the sentence is unambiguous, not when it is shortest. STE changes form, not substance. If the source has nothing to say, say so rather than polishing it into a clean but hollow paragraph.

### Voice

- Active voice is required for procedures and instructions.
- Use direct imperatives for procedural work steps, rather than narrative descriptions or passive requirements.
- Use active voice in descriptions as well. A descriptive passive is permitted when the actor is unknown, not merely because a known actor seems irrelevant. Apply [source fidelity](#source-fidelity) when the actor is unspecified.

### Sentence structure

- One instruction per sentence.
- Put a prerequisite before the work-step action when the reader needs that condition before acting. Do not treat this as a requirement to move every conditional clause in every descriptive sentence.
- Maximum 20 words per sentence for procedures and instructions. Maximum 25 words for descriptive text. Assess complete sentences across visual wrapping and each Markdown table cell in context.
- Do not omit sentence parts (verb, subject, article) just to shorten the sentence — the standard explicitly warns that this creates ambiguity rather than clarity.
- Noun clusters (strings of nouns stacked as a modifier) are capped at 3 words.
- Semicolons are not permitted at all (Rule 8.1): "You can use all standard English punctuation marks but not the semicolon (;)." Write separate sentences instead. Every other standard mark, including the em dash, remains permitted. Scan compound and subordinate clauses for run-on sentences; keep one idea per sentence even when its punctuation is permitted.

### Paragraph and document structure

- One topic per paragraph.
- Maximum 6 sentences per paragraph.
- Use a numbered or bulleted list for 3+ steps or conditions, and for complex enumerations, instead of burying them in prose.

### Framing and claims

- **Hedge stacking:** remove empty framing such as "it is important to note that this may potentially help to improve" while applying [source fidelity](#source-fidelity).
- **Marketing adjectives:** remove empty praise such as seamless, robust, powerful, cutting-edge, effortless, and blazing-fast. Retain substantive design and benefit claims as claims, and request evidence when needed. Use measurements only if supplied.

### Safety instructions

- Safety-critical instructions must open with a clear command or condition, not be buried mid-sentence.
- Some safety wording is controlled by legal or company requirements. Identify that constraint and obtain an authorized wording decision rather than silently changing it. A policy constraint does not itself prove STE compliance.

## Application and review responsibilities

STE is a technical-documentation standard for procedural and descriptive text across industries. It is not a general correspondence standard, an oral-communication standard, or an English-teaching method. Its principles can improve other writing and presentations, but an adaptation is not full-standard compliance. It is not part of the S-Series specifications.

Readers do not need STE training to benefit, but still need sufficient English comprehension. STE benefits native and non-native readers; it does not remove the need for translation when readers cannot understand English.

Writing STE requires strong English skills, knowledge of the technical subject, and an understanding of both the rules and the dictionary. C1 advanced English proficiency is recommended for writers, not imposed on readers. Authors remain responsible for approving edits; unresolved technical choices need author input.

## Completing strict-STE verification

Use the current published issue. Maintenance proposals are assessed before agreed changes appear in a later issue. Do not use a proposed word or sense as if it were already approved.

Obtain the standard through the [official Issue 9 request route](https://www.asd-ste100.org/STE_downloads.html#article02-2l). It is a request form that emails a PDF link, not a direct download. Check each proposed sentence against the full writing rules and each general word against its permitted meaning and part of speech. Verify technical nouns and verbs using the [technical-terminology criteria](#technical-terminology).

Resolve outstanding author decisions and apply the standard's word-counting rules. Have an STE-competent editor review grammar, technical meaning, and source fidelity together. Keep outputs provisional until those checks are complete.

[STEMG training guidance](https://www.asd-ste100.org/STE_training.html) identifies the standard as the indispensable reference. [STE support teams](https://www.asd-ste100.org/STEWorkingGroups.html) and [STEMG trainers](https://www.asd-ste100.org/STEtrainers.html) are consultation routes.

## Why This Skill Repurposes STE for Agent Output

STE was designed to eliminate ambiguity for a reader who cannot ask a follow-up question — a technician on a tarmac, working from a manual, with no author to call. An AI agent parsing another agent's output, a tool description, or a system message is in the same position: no back-channel to resolve "does this passive-voice sentence mean the caller does X, or the callee does X?" The same rule set that protects an airline mechanic from a misread torque spec protects a downstream agent from a misread instruction.

## Sources

- [ASD-STE100 official site](https://www.asd-ste100.org/)
- [ASD-STE100 — About STE](https://www.asd-ste100.org/about_STE.html)
- [STEMG training guidance — why the standard remains necessary](https://www.asd-ste100.org/STE_training.html)
- [Official Issue 9 request route](https://www.asd-ste100.org/STE_downloads.html#article02-2l)
- [ASD Europe — Simplified Technical English](https://www.asd-europe.org/standards-specifications/simplified-technical-english/)
- [Simplified Technical English — Wikipedia](https://en.wikipedia.org/wiki/Simplified_Technical_English)
- [TechScribe — ASD-STE100 Simplified Technical English](https://www.techscribe.co.uk/techw/asd-simplified-technical-english.htm)
- [SKYbrary — Simplified Technical English (STE)](https://skybrary.aero/articles/simplified-technical-english-ste)
