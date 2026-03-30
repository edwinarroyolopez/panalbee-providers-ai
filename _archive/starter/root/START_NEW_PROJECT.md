# Start a new product from this monorepo

High-level entrypoint for project setup. This file now delegates discovery/synthesis/generation behavior to `ai/setup/*.md`.

## 0) Clone and baseline

1. Clone/copy the starters you need (`template-web`, `template-app`, `template-backend`).
2. Read:
   - `ai/starter.md`
   - `ai/instructions/instructions.md`
   - `ai/agent-workflow.md`

## 1) Conversational setup (mandatory)

Use the setup engine:

- `ai/setup/start-new-project-flow.md` (master flow)
- `ai/setup/project-discovery-interview.md` (interview behavior)
- `ai/setup/project-discovery-question-bank.md` (question source)
- `ai/setup/project-synthesis-rules.md` (artifact synthesis)
- `ai/setup/project-generation-rules.md` (artifact creation policy)
- `ai/setup/project-completion-gate.md` (ready/not-ready gate)

Required behavior:

1. ask for free-form business prose first
2. summarize what is understood
3. ask only minimal missing questions
4. synthesize canonical context files
5. generate only necessary extra governance artifacts

## 2) Required setup outputs before feature work

Create these files in `ai/instructions/`:

- `project-context.md`
- `domain-map.md`
- `feature-map.md`
- `glossary.md`

Use `.template` files as structural references when useful, but drive content from conversational discovery.

## 3) Operational starter instantiation

After setup synthesis:

1. Wire environment
   - Web: `NEXT_PUBLIC_API_BASE` to your API root.
   - App: `template-app/src/config/apiBaseUrl.ts` dev/prod URLs.
2. Prune or quarantine example/legacy trees that are not product scope.
3. Align native IDs when release prep starts (Android app id, iOS bundle id, Firebase files).

## 4) Build phase

1. Treat generated context files as product source of truth.
2. Follow `ai/agent-workflow.md` for every implementation task.
3. Reuse/create agents/skills/workflows only when justified by generation rules.
4. Keep canonical starter semantics (`workspace`, `account`, `capability`, `tier`, `billingPlan`) unless your glossary explicitly defines a different product language.

## Workspace pattern (explicit)

In `template-web` and in the app shell, "workspace" means a scoped context under an account (aligned with `template-backend` `workspaces` on `/auth/me`). Legacy-heavy sample app code must stay under `template-app/src/quarantine/legacy-domain/` and out of starter-public/starter-protected/auth/system-design surfaces.
