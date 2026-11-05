# Website language

All product-owned, user-facing website content must be written in English. This applies to every route, including `/guide`, and to navigation, headings, explanations, examples of UI states, onboarding, buttons, tooltips, accessibility labels, empty states, errors, and cost summaries.

Write English directly in the source templates. Do not rely on runtime text replacement to translate the interface. Preserve original dataset/model proper names, source quotations, corpus text, and user-authored content; those may be in other languages.

When changing website content, check the affected rendered views and keep their language attributes consistent with the English interface.

# Spec-driven changes

Follow [docs/spec-flow.md](docs/spec-flow.md) for product behavior, API/SDK/worker contracts,
data, authentication, training, infrastructure, and cost-related changes.
Small typo, formatting, and documentation-only corrections may use the lightweight path
described there.

Research the current implementation first. Create `specs/YYYY-MM-DD-short-name/` from
`specs/_templates/`: `spec.md`, `plan.md`, `tasks.md`, and `verification.md`.
Give acceptance criteria stable `AC-*` identifiers and tasks `T-*` identifiers.
Distinguish facts, inferences, and unknowns; do not mistake proposed architecture for deployed code.

Obtain explicit user/reviewer approval of the spec and plan before implementation, and record
the decision in `plan.md`. Do not self-approve. Re-request approval when scope, contracts, or
material risks change. Mark tasks complete only after checking their results, and record actual
verification evidence for every acceptance criterion. Unrun tests are `NOT RUN`, not `PASS`.

Approval to implement does not authorize commits, pushes, deployments, production migrations,
or paid GPU operations. Request the relevant authorization separately unless already explicitly
provided. Never include credentials or private dataset content in specifications or evidence.
