# ASD-STE100 Writing Rules — Summary and Sources

This file summarizes the public, official description of ASD-STE100 (Simplified Technical English). It paraphrases rule *categories*. It does not reproduce the standard's text or its ~900-word dictionary verbatim. For the authoritative document, request the free download at the official site.

## Evidence and verification limits

Use the guidance below directly. It includes selected verified vocabulary restrictions, grammatical distinctions, and application limits, so applying those points does not require retrieving a web page.

This is not the complete Issue 9 standard or dictionary. The selected facts support only the restrictions stated, not approval of whole sentences. Other entries, rule numbers, exceptions, and the standard's word-counting method still require the full current standard. A whitespace count is not a verified STE count.

The skill's Strict/STE-flavored policies and its retained-compound-form fidelity exception are local adaptations, not ASD conformance levels or exceptions.

## What ASD-STE100 Is

ASD-STE100 is a controlled natural language, first released in 1986 (as AECMA Document PSC-85-16598) by what is now ASD (the AeroSpace and Defense Industries Association of Europe). It was built at the request of European airlines — most staffed by non-native English speakers — who needed maintenance documentation that could not be misread, because a misread instruction on an aircraft can kill people. The standard is maintained by the Simplified Technical English Maintenance Group (STEMG) and has been free to download since Issue 6 (2013). The current edition is Issue 9 (January 2025).

## Structure

- **53 writing rules across 9 sections** covering word choice, grammar, sentence structure, and style.
- **A dictionary** of roughly 900 approved words with restricted meanings and parts of speech, plus roughly 1,200 words to avoid with suggested replacements. Usually a word has one approved meaning and one approved part of speech; verify the actual entry rather than treating this as an exception-free rule.
- **A terminology allowance**: organizations may define their own dictionary of approved technical nouns and verbs beyond the base ~900 words, for domain-specific vocabulary the base dictionary can't cover.

## Rule Categories (Paraphrased)

### Word choice

- Use approved words only in their approved meaning and part of speech.
- Do not use another ordinary-English sense of a word merely because context makes it understandable.
- Choose the approved synonym, not just the one that seems plainest. Simplicity and frequency informed the vocabulary selection, but do not independently establish approval.
- Use an approved verb for an action, not a noun derived from that verb (Rule 3.7).
- Do not make phrasal verbs by putting a verb and a preposition together (Rule 9.3). Their meaning is not predictable from the parts, and non-native readers and translation systems both mishandle them.

Selected verified restrictions:

| Word | Apply this restriction |
|---|---|
| `start` | Use this selected verb instead of rotating among synonyms such as `begin`, `commence`, or `initiate`. |
| `check` | Approved as a noun, not as a verb. A construction such as "Do a check" uses the noun. Do not convert an approved noun into an unapproved verb to satisfy a preference for direct actions. |
| `fall` | The approved verb sense concerns gravity-driven downward movement, not a decrease in a quantity. |
| `about` | The approved sense concerns a topic, not numerical approximation. For an approximation, `approximately` or `around` can be approved alternatives when their intended sense fits. |

Approved meanings and spelling follow American English conventions based on Merriam-Webster. An ordinary dictionary can explain English, but it does not decide STE approval. Restrictions not covered here require the corresponding STE entry.

### Technical terminology

Technical nouns and technical verbs extend the controlled general vocabulary for a company, industry, or subject field. Establish their use from applicable documentation, engineering drawings, company glossaries, or terminology databases and the standard's subject-field categories.

A technical term can contain a word that is not approved independently in the general dictionary. This does not authorize that word outside the term, or make arbitrary jargon a technical term. Keep this use limited. A definition improves readability but is not, by itself, evidence of approved technical-term status.

Verify the term's intended meaning and use consistently. If its expansion, definition, or documented basis is missing, report that specific gap rather than inventing one.

### Verb forms

- Permitted forms include infinitive, imperative, simple present, simple past, simple future, and past participles as adjectives. Limited descriptive passive constructions also use past participles. Verify the permitted constructions against the complete standard.
- The secondary tense summary excludes present perfect: "We have received" becomes "We received" only when the meaning is equivalent. This is not a blanket prohibition of every auxiliary: simple future and permitted descriptive passives also need their applicable rules.
- Generally exclude "-ing" verb forms. Permitted uses include technical nouns or parts of technical nouns, and dictionary-approved nouns, adjectives, pronouns, or prepositions. For example, `opening` can be a noun and `remaining` an adjective; an ending alone does not identify a violation. Verify the actual part of speech and permitted sense.

### Voice

- Active voice is required for procedures and instructions.
- Use direct imperatives for procedural work steps, rather than narrative descriptions or passive requirements.
- Use active voice in descriptions as well. A descriptive passive is permitted when the actor is unknown, not merely because a known actor seems irrelevant. Preserve an unknown actor rather than inventing one.

### Sentence structure

- One instruction per sentence.
- Put a prerequisite before the work-step action when the reader needs that condition before acting. Do not treat this as a requirement to move every conditional clause in every descriptive sentence.
- Maximum ~20 words per sentence for procedures and instructions. Maximum ~25 words for descriptive text.
- Do not omit sentence parts (verb, subject, article) just to shorten the sentence — the standard explicitly warns that this creates ambiguity rather than clarity.
- Noun clusters (strings of nouns stacked as a modifier) are capped at 3 words.
- Semicolons are not permitted at all (Rule 8.1): "You can use all standard English punctuation marks but not the semicolon (;)." Write separate sentences instead. Every other standard mark, including the em dash, remains permitted.

### Paragraph and document structure

- One topic per paragraph.
- Maximum ~6 sentences per paragraph.
- Use vertical (numbered or bulleted) lists for sequences, conditions, or complex enumerations instead of burying them in prose.

### Safety instructions

- Safety-critical instructions must open with a clear command or condition, not be buried mid-sentence.
- Some safety wording is controlled by legal or company requirements. Identify that constraint and obtain an authorized wording decision rather than silently changing it. A policy constraint does not itself prove STE compliance.

## Application and review responsibilities

STE is a technical-documentation standard for procedural and descriptive text across industries. It is not a general correspondence standard, an oral-communication standard, or an English-teaching method. Its principles can improve other writing and presentations, but an adaptation is not full-standard compliance. It is not part of the S-Series specifications.

Readers do not need STE training to benefit, but still need sufficient English comprehension. STE benefits native and non-native readers; it does not remove the need for translation when readers cannot understand English.

Writing STE requires strong English skills, knowledge of the technical subject, and an understanding of both the rules and the dictionary. C1 advanced English proficiency is recommended for writers, not imposed on readers. Training or an STE-competent editor can help. Correct application preserves technical meaning; familiar-looking words and short sentences are not enough.

Checking tools are optional. Neither a clean tool result nor an AI opinion replaces the standard or an informed content review. ASD and the STEMG do not endorse or certify checker vendors. Authors remain responsible for approving edits, and unresolved technical choices need author input.

Use the current published issue. Maintenance proposals are assessed before agreed changes appear in a later issue. Do not use a proposed word or sense as if it were already approved. The standard is available without charge as a PDF through its official request route; that availability does not grant unrestricted redistribution rights.

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
