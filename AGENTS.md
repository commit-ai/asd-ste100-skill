# Repository architecture

This repository packages an English-rewriting skill and a deterministic Python linter.
The skill guides an agent's rewrites. The linter checks structural patterns, not meaning preservation or certified ASD-STE100 compliance.

- `skills/asd-ste100-skill/SKILL.md` owns triggers, routing, mode selection, and the rewrite workflow/output contract. Its frontmatter name is `asd-ste100`.
- `references/writing-rules.md`, within that skill directory, is the authoritative writing, fidelity, and verification policy.
- `references/review-workflow.md` owns review and supplied-fixes execution and the report contract.
- `examples/before-after.md` contains worked demonstrations and case-specific explanations, not general instructions.
- `scripts/ste-lint.py`, within that directory, contains the linter, CLI, and embedded regression tests. It uses only the Python standard library.
- `apm.yml` declares APM dependencies for Copilot and Claude. APM manages the local `.agents/`, `.claude/`, and generated assistant files. Change dependency declarations rather than installed copies.

# Commands

Run these commands from the repository root with Python 3.

Run the embedded regression suite:

```bash
python3 skills/asd-ste100-skill/scripts/ste-lint.py --selftest
```

Check one file, or supply several file paths:

```bash
python3 skills/asd-ste100-skill/scripts/ste-lint.py path/to/document.md
```

Check one input through stdin with structured output:

```bash
printf '%s\n' 'The request may have failed.' | python3 skills/asd-ste100-skill/scripts/ste-lint.py --json
```

For an isolated regression assertion, load the script with `runpy` and call `lint()`:

```bash
python3 -c 'import runpy; m = runpy.run_path("skills/asd-ste100-skill/scripts/ste-lint.py"); findings, _ = m["lint"]("- Set the target and"); assert [(f["rule"], f["line"], f["col"]) for f in findings] == [("dangling-conjunction", 1, 1)]'
```

The self-tests are assertions inside `selftest()`. Add linter regression cases there.

Check the skill document with the baseline documented in `README.md`:

```bash
python3 skills/asd-ste100-skill/scripts/ste-lint.py --baseline 40 skills/asd-ste100-skill/SKILL.md
```

The policy reference and worked examples quote patterns they discuss. Interpret findings in context.
`examples/linter-edge-cases.md` is intentionally invalid. The following command must exit 1 with exactly two `dangling-conjunction` findings:

```bash
python3 skills/asd-ste100-skill/scripts/ste-lint.py --json skills/asd-ste100-skill/examples/linter-edge-cases.md
```

# Skill conventions

Read `SKILL.md` and `references/writing-rules.md` before changing skill behavior. Read `references/review-workflow.md` when changing a review branch or its report contract.
Keep `README.md`, the skill, examples, and linter behavior consistent when a change affects their shared claims.

- Give each skill file one responsibility. Define each general language, fidelity, or verification policy once in `references/writing-rules.md`.
- Workflows and examples may link to or apply a policy, but must not redefine it. Keep case-specific explanations beside their examples.
- Keep task-specific steps and output contracts in their owning workflow document.

# Linter conventions

`lint(text, filename)` returns `(findings, words_total)`. Findings contain `file`, `line`, `col`, `rule`, `level`, `match`, and `message`.
Line and column numbers are one-based. Findings follow source order.

- `RULES` contains regex checks. Separate helpers handle sentence length, Markdown tables, and dangling list conjunctions. Synonym tracking resets for each file.
- Preserve source coordinates when masking inline code. Fenced code is skipped. Wrapped prose forms sentence blocks, while each Markdown table cell forms a separate block.
- The linter uses a 25-word cap. The skill's 20-word instruction cap requires context the linter cannot infer.
- Protect hedges and modal perfects such as "may have failed". Passive voice and compound tenses are advisory findings.
- Hard findings use the level `advisory-free`. The CLI exits 1 only when their aggregate count exceeds `--baseline`.
- Usage errors, unknown rule IDs, and unreadable files exit 2 through `argparse`. `--disable` accepts comma-separated rule IDs.
- JSON output contains `violations`, `count`, `hard_count`, `baseline`, `words`, and `per_100_words`. Keep this contract consistent with CLI tests.

When extending Markdown handling, preserve the supported syntax boundaries documented in `README.md`.
Keep the intentional fixture distinct from compliant examples.
