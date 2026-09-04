Decision Log
Decisions that would be costly or annoying to re-litigate, with the alternatives that were rejected and why.

Consult this when something in a later step appears to conflict with an earlier one — the reasoning here is usually the answer. Log a decision when it shapes the roadmap, the scope, or the architecture. Don't log every micro-choice.

Last updated: 2026-09-04

#	Date	Step	Decision	Why	Rejected alternatives
1	2026-09-04	Process	PROVISIONAL — confirm at handoff, don't assume. Where the code lives is decided when Step 9 closes, not before. Current leaning: a separate build repo, keeping this one pure planning.	Nothing during planning depends on the answer, and both options stay equally open until the end, so deciding early buys nothing. Put the choice to the user at handoff.	Neither option is rejected yet. Separate repo: planning stays uncluttered; the build agent can't see the planning files, so handoff docs must be self-contained. Same repo (planning moved to docs/planning/): docs sit next to the code and are likelier to stay current; the repo carries planning history the build doesn't need.
2	2026-09-04	Process	The build repo's documents are written fresh from the planning output, not copied.	Step files record how we decided, including dead ends and open questions; a coding agent loading that can't tell what's settled.	Copying the step files across — rejected as actively misleading to an agent.
3	2026-09-04	Process	The planning files freeze at handoff. Build-time discoveries are logged with the build, never back-ported into the step files.	Only one document set can be the live truth; back-porting creates two sources that disagree. Applies under either outcome of decision #1.	Keeping the plan living alongside the build — rejected because a stale spec that looks current is worse for an agent than one openly marked historical.
Reopened decisions
When an earlier decision is overturned, add a row above for the new call and record the reversal here.

Date	Original decision	What changed	New decision
—	—	—	—
