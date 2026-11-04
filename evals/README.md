# Verification

## v0.2.0 playlist workflow

Run [scenarios A–E](scenarios.md) in fresh chats with the skill loaded. Use only the fixture outputs. An independent agent exercised the workflow with simulated tool results:

| Scenario | Observed decision |
| --- | --- |
| Idea + daily updates | Resolved the musical brief, verified the seeded playlist, kept its URI, and created one matching schedule in the fixture. Initial creation counted for that local date. |
| Scheduler unavailable | Completed the authorized one-off playlist, then offered a schedule prompt and reported the unavailable scheduler. |
| Uncertain append, same date | Read the exact playlist, retained the frozen batch and did not add anything while the first request could still complete. |
| Connection changed | Stopped despite collaborator edit access. |
| Recommendations only | Returned a catalog shortlist without playlist or schedule changes. |

The review prompted a fix to require a documented private default or a supported private setting for direct creation. It also separated initial seeding of an empty playlist from verifying a generated playlist.

A live read-only catalog lookup verified the three public tracks in the README. The fixture checks exercise decisions. They do not verify live scheduled execution, account writes, or listener preference outcomes.

## Reproduce

Run each case with the same skill, fixtures and tool access. Compare the simulated calls and the reported result. Keep the recommended songs, failed writes, and scheduled task state distinct. Treat a missing receipt or an ambiguous write as unresolved. Cases 1–6 exercise earlier feedback, duplicate and connector boundaries.

To measure listener benefit, compare with a plain prompt using the same evidence, model, tools, and call budget. Hide candidate source labels during listening. Track both taste fit and meaningful exploration, and leave missing ratings unknown. [OpenAI guide to testing Agent Skills](https://developers.openai.com/blog/eval-skills)
