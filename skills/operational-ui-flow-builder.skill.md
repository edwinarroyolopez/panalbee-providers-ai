---
name: operational-ui-flow-builder
purpose: Build forms and operational flows consistent with the product’s UX language and existing components.
---

# Skill: Operational UI flow builder

## Why it exists

Daily work happens in screens, modals, selectors, timelines, and quick actions. Inconsistency here drives adoption risk and errors.

This skill follows a strict reduction-first UX bar: clarity, hierarchy, and operational speed over decorative complexity.

## What it solves

- Registration/edit/payment-style flows using proven patterns in **the current** codebase.
- Reuse of shared layout, loaders, attachments, and selectors.
- Clear feedback: loading, success, error, retry.

## When to use

- New operational screens.
- New mutation modals or sheets.
- UX adjustments without breaking the shared design language.

## Expected inputs

- Primary screen intention.
- Form fields and validations.
- Backend actions and response states.

## Internal steps

1. Define the dominant intention of the screen.
2. **Search `web-providers/src/components` (and `components/ui/`)** for existing primitives and compositions; reuse or extend before adding module-local UI.
3. Order hierarchy: context → primary action → detail.
4. Reuse patterns from reference modules only where domain-specific; otherwise prefer shared components.
5. Implement minimum validation for money, quantity, dates when applicable.
6. Immediate feedback and double-submit protection.
7. Integrate uploads when the flow needs evidence files.
8. Check empty/error/offline for critical actions.
9. Confirm the result does not read as starter/generic on operational surfaces.
10. For **primary operational screens**, add contextual help via the shared help modal pattern (purpose, decisions, how to operate, actions, expectations).
11. For **mass imports**, use the shared bulk-import panel + module hook: format copy, help, validation error list, phases, post-success reconciliation (refetch/poll), result summary—never a lone file input as the whole flow.

## Deliverables

- Working screen or modal aligned with the design system.
- Complete UX states (loading/success/error/empty).
- Copy and action consistency notes.

## Rules

- Do not introduce a parallel mini design system.
- **Mandatory reuse:** non-domain UI belongs in `web-providers/src/components`; do not duplicate selects, text areas, file inputs, modals, or badges inside modules without checking shared first.
- Avoid dense forms without hierarchy.
- Keep copy short, operational, and non-technical for end users.
- Reject UI that is merely functional but generic, noisy, or bureaucratic.
- Reject shipping active pages that still feel like the template starter.

## Acceptance check

Before closing UI work, confirm:

1. Primary action is obvious in seconds.
2. Visual hierarchy is effortless to scan.
3. Cards/modals/tables reduce cognitive load.
4. No redundant copy, controls, or styling noise remains.
5. The result feels like an intentional operational control surface.

## Common mistakes

- Multiple competing primary CTAs.
- Money/quantity inputs without consistent parsing.
- No visible confirmation after mutations.
