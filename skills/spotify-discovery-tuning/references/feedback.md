# Feedback and handoffs

Use the listener's words and the smallest state the workflow needs. Keep each track's verified identity, which round it appeared in, and separate judgments for artist familiarity, song familiarity, actual listening, liking, current suitability, and replay intent. Missing answers stay unknown. Update only the dimensions the user addressed.

| Listener says | Carry into the next round |
| --- | --- |
| “I know the artist. The song was new to me and I liked it.” | Keep the known-artist route and retain song unfamiliarity. Replay intent stays unknown. |
| “I still love that song, but I've heard it too much.” | Keep the liking and reduce this song temporarily. If no duration was given, the end date stays unknown. |
| “Good track, wrong for work.” | Retain liking and record a work-context mismatch. |
| “I skipped the third one.” | Retain the skip as an event. Leave liking and the reason unknown. If the order is ambiguous, ask for the title before recording track-specific feedback. |
| “Don't suggest that artist again.” | Apply the stated artist avoidance. Persist it only when requested and supported. |

When asked for a handoff, separate **what the user said**, **what the agent inferred**, and **what to try next**. For example, “They still like Track A and are tired of it. They gave no expiry. I omitted it in this round.” Keep only the evidence needed for the next round. Exclude account identifiers, device information, credentials, and unrelated history. Never mix users or silently merge imports across accounts.

For a comparative evaluation, give the skill and a plain-prompt baseline the same request, evidence, model, tools, and budget. Hide the condition labels during listening. Count only tracks the listener confirms were unfamiliar, played, liked, and worth revisiting. Leave missing responses unknown. Automated checks and agent judgments alone cannot measure preference lift.
