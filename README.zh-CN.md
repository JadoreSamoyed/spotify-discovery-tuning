# Spotify Discovery Tuning

**Spotify 又推同一首？从你熟悉的歌手里挖一首漏听的。**

[English](README.md) · [下载技能](https://github.com/JadoreSamoyed/spotify-discovery-tuning/releases/latest) · [安装到 Codex](#安装到-codex-项目) · [评估说明](evals/README.md)

![黑胶唱片上的两张反馈贴纸：听熟了、第一次听。](docs/launch-card.png)

## 看看第二轮怎么变

> **你：** 我喜欢 Arooj Aftab，但《Mohabbat》听腻了。还有什么可以试试？
>
> **第一轮：** 试试同张专辑的 [Last Night](https://open.spotify.com/track/3OBkjktMqs7QJ6dOUPWTji)。《Mohabbat》先放一放。
>
> **你：** 《Last Night》第一次听，很对味。继续找她的歌。
>
> **第二轮：** 试试 [Suroor](https://open.spotify.com/track/43li6JLxAxfmyVlHIbO9rn) 和 [Udhero Na feat. Anoushka Shankar](https://open.spotify.com/track/2hFN5GkZ1CNZNRp1tFYWqW)。保留这位歌手，换掉上一轮已经给过的歌。

*听众反馈为虚构示例，歌曲可在 Spotify 公开曲库找到。*

## 它会做什么

- 分开记录歌手是否熟悉、歌曲是否听过、推荐是否合适。
- 先给一小批，再根据具体反馈调整，延续已有的筛选依据。
- 有兼容的曲库工具时核验录音版本与 Spotify 链接，无法核验的内容会明确标注。
- 偏好调整默认只用于当前对话；保存偏好文件、创建或修改歌单，需要你明确提出。

这是对话中的选曲工作流，不会修改 Spotify 原生推荐算法。

## 安装到 Codex 项目

需要 Git，以及支持本地技能的智能体宿主。以下使用 Codex 的项目技能目录 `.agents/skills`。[Codex 官方技能文档](https://developers.openai.com/codex/skills/)

在准备使用技能的项目目录中执行：先克隆源码，阅读 `SKILL.md`，再复制技能文件夹。

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

安装后应存在 `.agents/skills/spotify-discovery-tuning/SKILL.md`。如果 Codex 未显示该技能，可重启 Codex。随后这样调用：

```text
$spotify-discovery-tuning
帮我找熟悉歌手唱的、我还没听过的歌。先给一小批，
需要哪些歌手或歌曲信息就先问我，再根据反馈调整。
```

## 曲库连接与核验

实时核验需要在智能体宿主中连接**兼容的 Spotify 曲库搜索或查询工具**。这个仓库提供技能指令，不包含 Spotify 连接器或访问凭据。

缺少工具时，技能会请你连接工具或提供 Spotify 链接，并明确说明核验状态。拿到链接不代表已经读过链接内容。仍然可以讨论选曲方向，但未经核验的候选不能写成已核实的曲库结果。

曲库核验确认“这是哪首、哪个版本”；你的反馈确认“这首对我是不是新歌”。

## 证据与适用范围

已有检查及其边界见 [评估说明](evals/README.md)。目前**没有实测的听众体验提升数据**，也不声称优于普通提示词。上面的对话展示预期行为，不是试听实验。

采用 [MIT 许可证](LICENSE)。独立社区项目，与 Spotify、OpenAI 无隶属关系。

如果它帮你挖到一首想再听的歌，可以点个 Star 方便下次找到。第二轮选偏了，也欢迎留下一条具体反馈。[提交反馈](https://github.com/JadoreSamoyed/spotify-discovery-tuning/issues/new)
