# Refactor Placement Rules

Use these rules when refactoring an existing skill.

## Decide Where Material Belongs

- Put deterministic command sequences, parsers, and validation steps in `scripts/`.
- Put fixed output scaffolding and variable text or artifact shapes in `templates/`.
- Put presentation assets, images, and other non-loaded output resources in `assets/`.
- Put longer explanatory guidance, schemas, and policy notes in `references/`.
- Put material in a shared folder only after multiple skills or roles have a concrete need to read it.
- Treat shared placement as the exception. Prefer one owning skill that other consumers invoke or reference.
- Skill and agent configuration guidance belongs with the owning skill unless it is clearly shared across roles.
- Decide shared placement by consumer read path, not file size: identify which consumers need the whole file, a section, or only a conditional reference.

## Choose Script vs Template

- Use a script when work is command-shaped, validation-heavy, or repeatedly retyped.
- Use a template when structure is stable but content still needs variables or short task-specific text.
- Keep prose when the value is judgment, exception handling, or context-dependent interpretation.
- If both apply, let the script cover mechanics and the template cover the human-facing payload.

## Keep Skill Bodies Lean

- Keep skill-specific resources under the owning skill.
- Extract repeated mechanics before rewriting them as prose.
- Do not surface an internal helper as a shared CLI or another role's tool without a concrete second consumer.
- Audit every shared reference by actual consumers. Prefer section-specific or conditional links when a consumer needs only one narrow rule.
