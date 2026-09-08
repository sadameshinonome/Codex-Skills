# Agent Guidance Test Policy

Use agent and skill tests only when they provide stable, mechanical evidence.
Do not use tests as a second copy of prose guidance.

## Keep

- Test executable helpers, parsers, generators, validators, hooks, and command wrappers through their real interfaces.
- Parse checked-in examples with the production schema when they are executable contract evidence.
- Check that local references and Markdown links resolve when broken paths would prevent skill use.
- Test runner discovery and other deterministic governance tooling.
- Keep deliberate line and word budgets for always-loaded or normal-path surfaces.
- Compare documentation with an executable authority only when it detects an interface mismatch rather than preferred wording.

## Remove Or Do Not Add

- Do not assert exact sentences, headings, paragraph order, synonyms, or preferred wording.
- Do not use required or forbidden keyword searches as a proxy for agent behavior.
- Do not duplicate prose policy in tests merely to prevent editing.
- Do not test judgment calls such as routing quality, review strictness, or whether prose sounds forceful.
- Do not keep permanent tests whose only purpose is proving a retired term or workflow is absent.
- Do not keep a test that fails after a semantically equivalent rewrite while executable behavior, structure, and context budget remain unchanged.

## Decision Check

Before adding or retaining a governance test, ask:

1. What executable behavior, machine-readable contract, path integrity, or quantitative budget does this prove?
2. Is there an authoritative implementation or measurable limit behind it?
3. Would a semantically equivalent prose rewrite leave the test green?

If the first two answers are unclear or the third answer is no, rely on skill review and real usage instead of a test.
