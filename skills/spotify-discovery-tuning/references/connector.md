# Spotify connector routing

Discover live tool schemas and use equivalent capabilities on other hosts. The Codex Spotify connector currently exposes these tools:

| Intent | Capability |
| --- | --- |
| Discover by mood, context, or taste | `spotify_search`. Use the listener's wording and original language within provider query rules. Inspect any playlist results before using their tracks. |
| Resolve known songs or URIs | `spotify_query_catalog` in batches with `MUSIC`, or `spotify_get_entity`. Match artist and recording version. Prefer returned canonical links. |
| Inspect an existing collection | `spotify_get_collection_items`. Use a known URI, check readiness and read all relevant pages before claiming complete coverage. |
| Make a playlist from an already selected list | `spotify_create_playlist`, then `spotify_add_playlist_items`. Confirm success and read back the exact target. The connector appends at the end. |
| Ask Spotify to pick and build from an idea | `spotify_generate_playlist`. Requires explicit playlist intent and an eligible Spotify Premium connection. It creates a private playlist. Check readiness and inspect the result before scheduling updates. |

For taste-shaped curation, first obtain a verified track list using catalog and discovery tools. When the connector supports direct creation and add, use that route to preserve the curated picks and their order. When the listener delegates song selection to the generator, pass their intent in their language without invented constraints. If a generator falls back because of the account plan, disclose the result. A request for a curated playlist can still be completed via independently supported create and add tools when those are authorized by the user's request and the host's tool rules.

A catalog match verifies identity. Track availability can depend on locale, account and restrictions. Exclude known blocked candidates. Leave missing availability unknown. Do not use a save status, track length, or incomplete listening history as proof that a song is unheard. [Spotify Recently Played](https://developer.spotify.com/documentation/web-api/reference/get-recently-played)

Reuse successful results on partial reads. Follow provider backoff for pending generation or rate limits. Bound further discovery and return fewer credible picks if necessary.

For the empty-playlist route, assemble the verified seed list before creating. Use a private visibility setting or a documented private default. If visibility is unknown, return the verified list and explain the setup needed for private creation. Once the empty playlist is created, save its URI in the current authorized context and add to that URI. For a generated playlist, read back its picks before deciding whether more tracks are needed.

On a timeout or ambiguous write result, read back the same target, or check whether a just-created playlist can be identified unambiguously. Preserve known successes. Retry only missing tracks when prior writes are settled and a complete read confirms what is missing. If the operation could still be in flight or the playlist cannot be identified, stop and report uncertainty. Do not create another playlist as recovery.
