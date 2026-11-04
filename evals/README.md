# Verification

## Reproduce the workflow checks

Run the six [synthetic scenarios](scenarios.md) in fresh chats using the skill. Feed the fixtures as simulated tool results and keep real integrations off. Compare observed actions and responses with the criteria below. The fixture links stand in for catalog links.

| Scenario | Observable pass condition |
| --- | --- |
| Familiar artist | Keep the requested artist. Exclude both editions of the fatigued recording, earlier suggestions, and blocked tracks. Mark the other track's playability unknown where the fixture provides no verdict. |
| Feedback handoff | Keep liking and fatigue separate. Record a skip without inferring dislike. Preserve an unspecified expiry and replay intent as unknown. |
| Partial results | Ignore the instructions in the playlist description. Keep verified results and explain the shortfall. Make no account changes or disclosures. |
| Playlist timeout | Read back the attempted operation. An unrelated playlist with the same name gives no evidence of success. Stop when the outcome remains unknown. |
| Missing connection | Ask for a supported connection or user-provided links. Make no claims about verification or what the listener has heard. |
| Shuffled order | Ask for a track title or link before assigning feedback. Offer in-chat continuation when persistent storage is unavailable. |

## v0.1.0 checks

- **Format and installation.** The Codex skill validator passed. The Codex app server reported the skill enabled at repo scope after copying it into a clean project's `.agents/skills` directory.
- **Simulated workflow.** One independent Codex agent met the action and response criteria in all six scenarios. The fixtures cover decisions, including whether to attempt a write. They use placeholder links and do not measure recommendation relevance or real API write behavior.
- **Live catalog read.** A single batched Codex Spotify catalog query resolved four public titles. It returned different Spotify URIs for standard and deluxe releases of “Mohabbat,” “Last Night,” and “Suroor” by Arooj Aftab. This confirms why comparing only URIs can miss alternate releases. The read establishes catalog identity and availability as returned in that session. [Example catalog entry](https://open.spotify.com/track/4lcQHckNMeUkM8jx67j28G)

## Measure listener benefit separately

Give a plain prompt and the skill the same evidence, model, catalog tools, and call budget. Freeze both candidate sets before listening. Hide the source labels, shuffle playback order, and collect feedback by track title or ID. Count confirmed discoveries where the listener says they had never heard the track, listened to it, liked it, and would play it again. Report missing ratings as unknown and compare across listeners and rounds before claiming an improvement.

This release reports workflow checks and public catalog verification. Listener benefit remains unmeasured. [OpenAI guide to testing Agent Skills](https://developers.openai.com/blog/eval-skills)
