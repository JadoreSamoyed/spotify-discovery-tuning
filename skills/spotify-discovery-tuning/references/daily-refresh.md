# Daily refresh

Create a recurring task only when the listener asks for recurring updates. A single request can authorize both playlist creation and the schedule. For an existing playlist, use its exact Spotify URI. A name alone is insufficient when matches are ambiguous.

## Set it up

1. Verify that the playlist exists, is editable with the intended connection, and contains the intended initial picks, or has a verified current state for an existing playlist. Preserve its returned URL.
2. Resolve cadence, local time and time zone. Use requested values. For “daily” without a time, use 08:30 in the listener's known time zone and report it. Ask for the time zone if it is unknown. Default to five additions per daily run. Follow any explicit amount or exclusions.
3. Discover the host's scheduler and check that the scheduled runtime can access the skill, the same account-scoped Spotify connection, the target playlist, and private continuity state. Use a verified account binding when exposed, or a host-scoped connection known to remain the same. Editability alone cannot identify the account because collaborators can also edit. If the runtime, connection, or private state cannot be verified, give a ready-to-use schedule prompt and say what still needs setup.
4. Before enabling the task, save a brief in private state with taste anchors, exploration routes, exclusions, exact playlist URI and URL, daily count, time zone, the refresh rule, and the verified seed date. In Codex, prefer the current chat's recurring task when available. Look up an existing task for the same user and playlist. Create once or update the matching task as requested. Save its confirmed ID. If creation times out, look for the task before retrying. [Codex scheduled tasks](https://learn.chatgpt.com/docs/automations?surface=app)

## On each scheduled run

- Verify the connection and exact target. Read all playlist pages needed for deduplication. Stop on a changed account, ambiguous permission, incomplete read, or revoked access. Use the schedule's local calendar date as the run key. Treat a verified seed on that date as the first refresh.
- Use the host's serialization or a per-playlist lock if concurrent runs are possible. A complete private receipt for that date ends the run. For an unfinished attempt, reconcile its frozen batch with a fresh playlist read before considering any new write. Wait or report uncertainty if an earlier write may still be in flight. When continuity or concurrency cannot be controlled, skip the write and report the blocker.
- Select up to the agreed number of verified new tracks across the brief's exploration routes. Exclude tracks already in the playlist and likely alternate releases of the same recording. Use recent run receipts to avoid immediate repeats. If no candidates fit, record a no-op.
- Save the frozen batch and an attempt marker before writing. Append to the same playlist by default. Keep existing tracks and the listener's edits. Never create a fresh playlist in a refresh run. Removal or rotation needs a separate explicit request and matching host capability. Re-read after the append, verify the additions and record the result. Treat uncertain responses as described in [connector routing](connector.md).
- Use the user's notification preference. For a quiet schedule, report meaningful changes and actionable blockers according to the host's notification settings. Use the actual scheduler to pause or update the task when asked.

## Example recurring task prompt

> Use $spotify-discovery-tuning for my playlist at <verified playlist URI>. Each day, add up to five verified picks that suit a rainy-night walk. Keep post-punk and hazy guitar textures as anchors, with nearby artists and sounds where they fit. Skip tracks already in the playlist, check alternate releases, and preserve existing tracks. Read and verify the same playlist before and after writing, and use the private run receipt to prevent duplicate daily updates. If the connection, playlist or outcome cannot be verified, report what needs attention.
