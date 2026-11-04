# Spotify Discovery Tuning

**One idea. A Spotify playlist shaped by your taste, with new picks every day.**

[简体中文](README.zh-CN.md) · [Download the skill](https://github.com/JadoreSamoyed/spotify-discovery-tuning/releases/latest) · [Install](#install-in-codex) · [Verification](evals/README.md)

![One idea leads to a Spotify playlist and daily additions that fit the same taste.](docs/launch-card.png)

## Give it one idea

> Make me a rainy-night walking playlist. Keep my post-punk taste and hazy guitars, but branch out. Add five new tracks to the same playlist every morning at 8:30, Asia/Shanghai.

The agent uses your brief to look in three directions. In this example, it digs deeper into a familiar artist with [Primary · The Cure](https://open.spotify.com/track/4fnx6Wman02ryvAOqKm6iI), moves to a related band with [Second Skin · The Chameleons](https://open.spotify.com/track/5F43dz91uj1bQRKDvXbt1f), and explores a neighboring sound with [Lorelei · Cocteau Twins](https://open.spotify.com/track/1ZnXuijpwEBjhNxpEnb8WH). Each direction stays tied to the brief.

With the needed tools and your request, the agent creates a private Spotify playlist and schedules daily additions to that same playlist. It checks for duplicates before adding, keeps existing tracks, and gives you the playlist link and schedule. A later instruction such as “more bass, fewer slow tracks” can tune future picks.

*Illustrative brief and workflow. The tracks were checked in the public catalog. The example does not create a playlist or schedule.*

## Install in Codex

From your project with Node.js 22.20+ and Git:

```bash
npx skills add JadoreSamoyed/spotify-discovery-tuning --skill spotify-discovery-tuning --agent codex --copy
```

Or extract the [release ZIP](https://github.com/JadoreSamoyed/spotify-discovery-tuning/releases/latest) into `.agents/skills` so that `.agents/skills/spotify-discovery-tuning/SKILL.md` exists. Connect Spotify to the host and open Codex in the project. Type `$spotify-discovery-tuning` and paste your listening idea.

| Use case | What the agent needs |
| --- | --- |
| Preview picks | Spotify catalog read access |
| Build a Spotify playlist | Spotify playlist create and add access, or an eligible playlist generator |
| Keep the same playlist fresh | A supported scheduler with access to the skill, the same authorized playlist connection, and private run state |

The agent creates the schedule only when you ask for recurring updates. In Codex, use a chat with Scheduled available. A task that needs local skill files or run state needs the computer and app running. Check the first scheduled run in your host. [Codex scheduled tasks](https://learn.chatgpt.com/docs/automations?surface=app)

See [the skill](skills/spotify-discovery-tuning/SKILL.md) and the [daily refresh rules](skills/spotify-discovery-tuning/references/daily-refresh.md) for the full workflow and fallback behavior.

[MIT license](LICENSE). If it helped you build a playlist worth keeping, star the repo or share the idea that worked. [Issues](https://github.com/JadoreSamoyed/spotify-discovery-tuning/issues)
