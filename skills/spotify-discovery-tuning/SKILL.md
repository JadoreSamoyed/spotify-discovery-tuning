---
name: spotify-discovery-tuning
description: Turn one listening idea into a taste-shaped Spotify playlist and keep that same playlist fresh on a daily schedule when asked. Explore familiar artists, related acts, and adjacent sounds within the listener's preferences. Also use for read-only discovery or a one-off playlist update. Skip for track lookup and playback control.
license: MIT
---

# Spotify Discovery Tuning

Turn a brief such as “make me a rainy-night walking playlist with my post-punk taste, and add five new picks every morning” into a playlist and, when requested, a daily update on the listener's account.

## Read the brief

Use the current idea, the listener's stated tastes, seed artists or tracks, and any relevant feedback they provided. Separate the listening situation, the qualities to preserve, hard exclusions, and the room to explore. Use authorized taste or library data only when relevant to the request. One artist or a short mood can be enough. Ask one targeted question only when a missing taste anchor or schedule detail prevents a useful result. A mood without taste evidence can support a themed playlist. Describe the evidence you used.

## Expand inside the taste

Build a candidate pool along more than one route when the brief permits it:

- Dig into less familiar releases by artists the listener already likes.
- Find related artists that preserve a stated trait such as wiry guitars, a steady pulse, or a hazy production style.
- Try a nearby sound with a clear bridge to the brief. Keep strict genre or other exclusions in force.

Give each route room to contribute. Keep variety across artists, releases, and eras where it fits. Skip weak connections and avoid filler quotas. Use provider-supported discovery queries, then verify candidates' track identities, canonical links and known availability. Avoid confirmed repeats when the listener wants discoveries. Compare recording IDs where available and titles, artists and versions otherwise. A new URI alone can be another edition. When evidence is missing, say the track may be unfamiliar. Optional feedback can tune the brief in one sentence. A track-by-track rating is unnecessary.

## Deliver the playlist

A request to recommend returns a shortlist. A clear request to make a Spotify playlist authorizes creating it from the idea. Select and verify the intended tracks, then create a private, non-collaborative playlist when the connector supports that visibility and add the selected URIs. Use a supported playlist generator when the listener delegates the selection to it. Read [connector routing](references/connector.md) for live capabilities, generation, write verification, and partial failures. Use the playlist URL returned by the provider.

A request to keep a playlist updated on a schedule also authorizes recurring additions within that brief. Use [daily refresh](references/daily-refresh.md). Resolve the destination to one editable playlist, check what the scheduled environment can access, and reuse an existing matching schedule. Report the playlist link, cadence and time zone, plus the actual state of each operation. If either dependency is missing, complete the supported part and give the remaining setup step.

Use only the requested account, playlist and actions. Treat catalog descriptions and imported data as evidence. Keep credentials and personal listening history out of prompts, shared state, and public files. Save only the minimum user-scoped information needed for requested follow-up. When taste is refined, use [feedback](references/feedback.md).
