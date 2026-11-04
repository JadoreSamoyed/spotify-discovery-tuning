# Spotify capabilities

Discover the current tool schemas before using the names below. These are capability mappings for the Codex Spotify connection. Other hosts can use equivalent tools.

| Need | Codex Spotify capability | How to use it |
| --- | --- | --- |
| Discover from a listening request | `spotify_search` | Preserve the user's language and wording, applying only transformations the tool allows. Do not pass real names, handles, or unrelated user data. |
| Verify a known title and artist | `spotify_query_catalog` | Use `MUSIC` and batch distinct lookups within the live limit. Compare artist and release when names match. Use discovery tools for moods and similarity. |
| Resolve a known Spotify URI | `spotify_get_entity` | Use tool-returned or user-provided identifiers. Prefer the canonical link from the result. |
| Inspect a returned playlist or album | `spotify_get_collection_items` | Read from its known URI. Respect pagination, provider polling rules, and the round's read budget. |
| Create a requested playlist | The connector's playlist write tools | Reuse verified tracks, preserve requested order, and read back if supported. A permission field or read-only generated result does not authorize a write. |

Read per-item warnings and errors. Preserve good results on partial failure. Retry a transient read failure once, within the round's budget and provider backoff. Stop on authorization or region restrictions. If the connector returns only a pending generated playlist and the budget is spent, report the limitation or finish with already verified tracks.

A playlist write that times out has an unknown outcome. Check the target playlist or account for the attempted change before retrying. If the outcome remains uncertain, report that uncertainty and stop to avoid duplicate playlists or tracks.

A catalog match verifies identity. Playability can depend on locale, account, and restrictions. Use `PLAYABLE` only where returned, preserve known restrictions, and leave unspecified status unknown. A search response can include a generated playlist with `NOT_SAVED`. Inspect its contents before recommending from it.

`playback.duration_ms` is track length. `display.played_ms` describes position for supported spoken content. Neither records music listening events. The Recently Played endpoint is a separate integration with bounded coverage. A user-provided export also covers only the accounts, dates, and services it describes. [Spotify Recently Played](https://developer.spotify.com/documentation/web-api/reference/get-recently-played) · [Understanding Spotify data](https://support.spotify.com/us/article/understanding-your-data/)

Spotify's own Taste Profile controls have their own documented scope. Suggest them only if the user asks about native recommendations. [Spotify Taste Profile](https://support.spotify.com/us/article/your-taste-profile/)
