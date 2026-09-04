# Step Guide
Reference for each of the 9 steps: what to ask, when the step is actually done, and what usually goes wrong.
Read the relevant section when starting a step, and again before proposing to close it.

Last updated: 2026-09-04

---

## Step 1 — Start from your goal
**Key questions**
- Why does this need to exist? What breaks or stays painful if it doesn't?
- Who *specifically* is it for? Narrow enough to name a real person who fits.
- What do those people do today instead, and why is that unsatisfying?
- What makes this genuinely valuable — stated as a change in the user's outcome, not a feature list?

**Done when**
- The target user is specific, not a category like "businesses" or "everyone".
- The "why" survives "…and why does that matter?" asked twice.
- Value is expressed as an outcome that changes for the user, with the current alternative named.

**Traps**
- "Everyone" as the audience, or a user segment so broad it constrains nothing.
- Describing the solution instead of the problem.
- "It's faster/easier" with no baseline to be faster than.

---

## Step 2 — Define user capabilities & features
**Key questions**
- What can a user *do*? Phrase every item as a user action, not a component.
- What must the system deliberately prevent, limit, or refuse?
- What is explicitly out of scope, even though someone will ask for it?
- Which single capability is the one the whole thing exists for?

**Done when**
- Every feature reads as a user capability ("a user can…"), not a noun like "dashboard" or "database".
- Guardrails and limitations are written down, not just implied.
- No technology is named anywhere.

**Traps**
- Listing system components instead of user capabilities.
- Quietly adding admin, reporting, or settings features nobody asked for.
- Leaving permissions and limits until "later" — they shape Steps 3 and 5.

---

## Step 3 — Define the data models
**Key questions**
- What entities exist, and what does each one need to hold?
- How do they relate, and with what cardinality (one-to-many, many-to-many)?
- Who creates, owns, edits and deletes each record?
- What's the lifecycle — does anything expire, archive, or get soft-deleted?

**Done when**
- Every Step 2 capability can be traced to entities that support it.
- Relationships have explicit cardinality.
- No orphan entities that no capability actually needs.
- Ownership and visibility are defined per entity.

**Traps**
- Modelling for imagined future features.
- Choosing a database or naming field types in DB-specific terms — that's Step 8.
- Forgetting who is allowed to see each record.

---

## Step 4 — User flow & UI mapping
**Key questions**
- What screens or views exist?
- What is the exact path from arriving to completing the core action?
- What does a brand-new user with no data see?
- Where can someone get stuck, confused, or lost?

**Done when**
- The primary flow is mapped end to end, screen by screen.
- Every screen maps to at least one Step 2 capability.
- Entry/auth, empty states, and error states are covered — not just the happy path.

**Traps**
- Designing visuals (colors, layout) instead of flow and structure.
- Only mapping the happy path.
- Screens that exist out of habit and serve no capability.

---

## Step 5 — System architecture & core logic
**Key questions**
- What are the major components and what is each one responsible for?
- What operations must the backend expose to support Step 4's flows?
- Where does the core logic actually live?
- What external systems or third parties are involved?

**Done when**
- Each Step 2 capability traces to a specific operation.
- Every component has a single, clearly stated responsibility.
- External dependencies and integrations are named.
- Still no frameworks or product names.

**Traps**
- Over-engineering: queues, microservices, and caching layers for something with ten users.
- Under-estimating: "auth" or "sync" as a single hand-waved box hiding weeks of work.
- Naming technology — redirect to Step 8.

---

## Step 6 — Scope & MVP definition
**Key questions**
- What is the smallest version that still delivers the Step 1 value?
- What gets cut, and to which later phase?
- Which one thing must work *really* well for this to be worth using?
- What would we regret shipping without?

**Done when**
- Every Step 2 feature is explicitly classified as MVP or deferred.
- The MVP still delivers the Step 1 value proposition — check this directly.
- The cut list is written down, not deleted, so it stops resurfacing.

**Traps**
- An "MVP" that contains everything.
- Cutting the one capability that makes the project distinctive.
- Deferring the hard thing that the whole value depends on.

---

## Step 7 — Presentation layer
**Key questions**
- What form does this take — web app, mobile app, desktop, CLI, script, extension?
- Where are users physically when they use it, and on what device?
- Does it need to work offline, or on a phone, or alongside another tool?
- What does this form imply for Step 5's architecture?

**Done when**
- The form is chosen with reasoning tied back to Steps 1 and 4.
- Implications for architecture are noted, and Step 5 updated if needed.
- One primary form for the MVP, not three.

**Traps**
- Choosing by habit rather than by where the user actually is.
- Committing to web + iOS + Android for v1.
- Letting this slide into framework choice — that's still Step 8.

---

## Step 8 — Tech stack selection
**Key questions**
- What do Steps 3, 5 and 7 actually *require* from the stack?
- Where will this be deployed and hosted, and what does that constrain?
- What does whoever's building it already know well?
- What's boring, stable, and well-documented enough to still work in two years?

**Done when**
- Every choice is justified by a specific requirement from an earlier step.
- The deployment path is concrete, not "we'll figure out hosting later".
- Nothing was chosen because it's new or interesting.

**Traps**
- Picking the stack first and back-filling the justification.
- Résumé-driven choices.
- Ignoring the ops cost — hosting, migrations, secrets, backups.

---

## Step 9 — The development process
**Key questions**
- What's the folder structure and the naming conventions?
- What environments exist (local, staging, production) and how do they differ?
- What's the git workflow — branches, commits, reviews?
- What gets built first, and what's the first slice that works end to end?
- **What are the exact commands to install, run, test, and lint?** Write them literally.
- How does someone — human or agent — verify a change actually works before committing it?
- Where do secrets and config live, and how does a fresh checkout get running?

**Done when**
- Repo structure and conventions are written down explicitly.
- Environment and version-control workflow are defined.
- Build order is sequenced so something works end to end early, rather than all infrastructure first.
- The install / run / test / lint commands are written down verbatim, not described.

**Traps**
- Building all the scaffolding before any user-visible capability.
- No first vertical slice, so nothing is demonstrable for weeks.
- Leaving conventions implicit and "obvious".
- Finishing the step without concrete commands. An agent with no command list guesses, fails, retries — and sometimes reports success without having run anything. This is the single most valuable thing Step 9 produces.

---

## Handoff — after Step 9
Planning ends here and building begins.

**First, put this choice to the user — it is deliberately left open until now:**

| | Separate build repo | Same repo, planning moved to `docs/planning/` |
|---|---|---|
| Planning files | Stay put, frozen | Move into `docs/planning/` |
| Upside | Build repo starts clean, no planning history | Docs sit beside the code, likelier to stay current |
| Cost | The build agent can't see the planning files at all, so handoff docs must be fully self-contained | Repo carries planning history the build doesn't need |

Either way the rest of this section applies unchanged; only the destination differs.

**The documents below are written fresh from the planning output — not copied.** The step files record *how* we decided, including dead ends and open questions. A coding agent loading that gets confused about what's actually settled. It needs *what was decided*, stated once, cheap to load.

### Build output set
| File | Built from | Purpose |
|---|---|---|
| `CLAUDE.md` (build version) | Step 9 | Role, conventions, guardrails, and the install/run/test/lint commands |
| `SPEC.md` | Steps 1, 2, 6 | What it is, who it's for, capabilities marked MVP vs. deferred |
| `DATA-MODEL.md` | Step 3 + Step 8 | Entities, fields, relationships — concrete now the database is chosen |
| `ARCHITECTURE.md` | Steps 5, 7, 8 | Components, operations, stack |
| `DECISIONS.md` | `00_decisions.md` | Carried over near-verbatim — stops settled calls being reopened |
| `BACKLOG.md` | Step 9 | Build order as actionable work, first vertical slice first |

Flows and screens from Step 4 go into `SPEC.md` or their own file, whichever keeps `SPEC.md` readable.

### Left behind
`00_step-guide.md`, `00_progress-tracker.md`, `00_project-overview.md`, the numbered step files, and every "Open questions" and "Revision history" section. They're planning process, not build input.

### Handoff checklist
1. Confirm all 9 steps are `Final`.
2. **Put the repo choice above to the user.** Then either create and name the build repo, or move the planning files into `docs/planning/` here.
3. Write the six documents above from the planning output — fresh prose, not copy-paste.
4. Verify the build `CLAUDE.md` contains the literal commands from Step 9.
5. Note in `README.md` that planning is complete and where the build lives.
6. Record the repo decision in `00_decisions.md`, replacing the provisional entry #1.
7. Mark the planning files frozen.

If the build uses a spec-driven toolkit (GitHub Spec Kit or similar), ask before writing the output set — some of it maps onto that tool's own artifacts and shouldn't be hand-written twice.

### Freeze rule
After handoff the planning files are a historical record. When the build reveals the plan was wrong — and it will — that gets fixed and logged **with the build**. Never back-port it into the step files. Only one document set can be the live truth.
