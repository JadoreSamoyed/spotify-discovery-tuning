# Spotify Discovery Tuning

**Find tracks you may have missed by artists you already like.**

[简体中文](README.zh-CN.md) · [Skill](skills/spotify-discovery-tuning/SKILL.md) · [Evaluation notes](evals/README.md)

An instruction-only agent skill for music discovery when recommendations keep circling back to the same songs. It treats **knowing an artist** and **knowing a track** as separate signals, then uses your feedback to refine the next small batch.

## Two turns, one useful correction

*Synthetic illustration of the workflow. No real listener, track recommendations, or live verification results are represented here.*

**Turn 1**

> **You:** Find songs I haven't heard by artists I already know. Don't keep returning their biggest hits.
>
> **Assistant:** I'll keep those artists in scope, exclude songs you've already identified as familiar, and start with a small batch. I'll label which track details I can verify; whether you've heard a song is still for you to confirm.

**Turn 2**

> **You:** Candidate A is familiar. Candidate B is new to me and fits. More in that direction.
>
> **Assistant:** I'll exclude A and use B to guide the next batch. Familiar artists remain eligible; your feedback changes which tracks I look for.

## What the skill does

- Separates artist familiarity, track familiarity, and whether a recommendation fits.
- Refines a small batch using concrete feedback instead of restarting from a generic recommendation request.
- Checks recording identity and Spotify links when compatible catalog tools are available, and labels anything it cannot verify.
- Keeps working preferences in the current conversation by default. Saving a preference file or creating or changing a playlist requires an explicit request.

This is a conversational workflow. It does not change Spotify's native recommendation algorithm.

## Install in a Codex project

Requires Git and an agent host that supports local skills. The commands use Codex's project skill directory, `.agents/skills`. [Official Codex skill guide](https://developers.openai.com/codex/skills/)

Run from the project where you want to use the skill. Clone the source, read `SKILL.md`, then copy the skill folder.

<details>
<summary>Bash</summary>

```bash
git clone https://github.com/JadoreSamoyed/spotify-discovery-tuning.git spotify-discovery-tuning-source
cat spotify-discovery-tuning-source/skills/spotify-discovery-tuning/SKILL.md
mkdir -p .agents/skills
cp -R spotify-discovery-tuning-source/skills/spotify-discovery-tuning .agents/skills/
```

</details>

<details>
<summary>PowerShell</summary>

```powershell
git clone https://github.com/JadoreSamoyed/spotify-discovery-tuning.git spotify-discovery-tuning-source
Get-Content -LiteralPath './spotify-discovery-tuning-source/skills/spotify-discovery-tuning/SKILL.md' -Raw
New-Item -ItemType Directory -Force -Path './.agents/skills' | Out-Null
Copy-Item -LiteralPath './spotify-discovery-tuning-source/skills/spotify-discovery-tuning' -Destination './.agents/skills/' -Recurse
```

</details>

The resulting file should be `.agents/skills/spotify-discovery-tuning/SKILL.md`. If the skill does not appear in Codex, restart Codex. Invoke it with:

```text
$spotify-discovery-tuning
Help me find unfamiliar tracks by familiar artists. Start with a small batch,
ask for the artists or tracks you need, and refine it from my feedback.
```

## Catalog access and verification

Live verification requires **compatible Spotify catalog search or lookup tools connected to your agent host**. This repository supplies instructions, not a Spotify connector or credentials.

If the tools are unavailable, the skill asks for a connection or Spotify links and clearly labels the verification status. A supplied link alone is not proof that its contents were checked. You can still discuss what to look for, but unverified candidates must not be presented as verified catalog results.

Catalog verification establishes what a recording is. Your feedback establishes whether it is unfamiliar to you.

## Evidence and scope

See [evaluation notes](evals/README.md) for the available checks and their limits. There is **no measured listener uplift** and no claim that this skill outperforms an ordinary prompt. The demo above illustrates intended behavior, not a listening experiment.

[MIT license](LICENSE). Independent community project; not affiliated with Spotify or OpenAI.
