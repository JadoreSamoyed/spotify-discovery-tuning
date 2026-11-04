# Spotify Discovery Tuning

**从喜欢的歌手里找可能漏听的歌。**

[English](README.md) · [技能文件](skills/spotify-discovery-tuning/SKILL.md) · [评估说明](evals/README.md)

当推荐总在同几首歌里打转，这个纯指令型智能体技能会把**熟悉歌手**和**听过歌曲**分开判断，再根据你的反馈调整下一小批推荐。

## 两轮对话，让反馈真正影响下一批

*以下是合成示例，仅展示工作方式，不代表真实听众、实际曲目推荐或在线核验结果。*

**第一轮**

> **你：** 想听熟悉歌手唱的、我还没听过的歌，别总给我他们最热门的那几首。
>
> **助手：** 我会保留这些歌手，排除你已明确听过的歌曲，先给一小批候选。曲目资料能否核验会单独标明；你有没有听过，仍需要你的反馈。

**第二轮**

> **你：** 候选 A 听过了。候选 B 没听过，而且对味，再沿这个方向找。
>
> **助手：** 下一批排除 A，用 B 的反馈来调整方向。熟悉的歌手仍然可以入选，变化的是具体找哪些歌。

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
