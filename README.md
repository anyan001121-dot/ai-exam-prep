# AI 求职复习包

`ai-exam-prep` 是一个采用 [Agent Skills 标准](https://agentskills.io/specification) 的求职备考技能。给它公司和岗位名，或贴一份岗位描述（JD），它会用当前工具的网页搜索能力找公开笔经和面经，核对原帖，再整理成带出处的考点总表、学习计划和练习题。

适用于校招、实习和社招。你可以从岗位摸底一路做到限时练习，也可以只查一轮面试、学一个模块或讲一道题。

[查看腾讯算法工程师复习包示例](examples/tencent-algorithm-engineer.md) · [查看技能指令](SKILL.md)

## 安装与更新

同一份 `SKILL.md` 可用于下面的工具。安装技能只需要这个文件。**自动搜帖需要当前会话能搜索网页，核对原帖需要能打开网页。** 工具暂时无法联网时，也可以提供已有经验帖、JD 或考试通知，让技能继续整理复习资料。

### Claude 网页版

下载 ZIP 后保持压缩状态。在 Claude 的自定义技能管理中选择上传，启用 `ai-exam-prep`。如果看不到上传入口，可以在设置中检查代码执行和文件创建功能是否开启，以及账号是否允许自定义技能。[下载 Claude 安装包](https://github.com/anyan001121-dot/ai-exam-prep/releases/latest/download/ai-exam-prep.zip) · [Claude 官方安装说明](https://support.claude.com/en/articles/12512180-use-skills-in-claude)

### Codex、Claude Code、Cursor、VS Code 和 OpenCode

下载 `SKILL.md`，按下表放到选定目录。`~` 表示用户主目录。用项目目录安装时，从项目里打开聊天。[打开技能文件](SKILL.md)

| 工具 | 用户级安装路径 | 调用方式 |
| --- | --- | --- |
| Codex | `~/.codex/skills/ai-exam-prep/SKILL.md`，自定义 `CODEX_HOME` 时用该目录下的 `skills/` | 在聊天中选择 `$ai-exam-prep` |
| Claude Code | `~/.claude/skills/ai-exam-prep/SKILL.md` | 输入 `/ai-exam-prep`。[官方文档](https://code.claude.com/docs/en/skills) |
| Cursor | `~/.cursor/skills/ai-exam-prep/SKILL.md` | 在 Agent 聊天里选择 `/ai-exam-prep`。[官方文档](https://cursor.com/docs/skills) |
| GitHub Copilot（VS Code） | `~/.copilot/skills/ai-exam-prep/SKILL.md` | 在 VS Code Chat 中选择 `/ai-exam-prep`。项目级路径为 `.github/skills/ai-exam-prep/SKILL.md`。[官方文档](https://code.visualstudio.com/docs/agent-customization/agent-skills) |
| OpenCode | `~/.config/opencode/skills/ai-exam-prep/SKILL.md` | 在聊天里说「用 ai-exam-prep 帮我准备……」。[官方文档](https://opencode.ai/docs/skills/) |

也可以用 Git 把仓库直接克隆到相应的 `ai-exam-prep` 目录。例如在 macOS 或 Linux 上安装到 Codex：

```bash
git clone https://github.com/anyan001121-dot/ai-exam-prep.git "${CODEX_HOME:-$HOME/.codex}/skills/ai-exam-prep"
```

通过 Git 安装后，在对应技能目录运行 `git pull --ff-only` 更新。手动安装时替换 `SKILL.md`。更新后开启新聊天，确认可以选中或调用技能。

### OpenClaw

用内置命令把技能安装到当前工作区，更新时再次运行安装命令。[OpenClaw 官方文档](https://docs.openclaw.ai/tools/skills)

```bash
openclaw skills install git:anyan001121-dot/ai-exam-prep@main
```

## 快速开始

提供**岗位方向**就可以开始。加上公司、团队、招聘类型或届次，有助于找到更匹配的经验帖。已有考试通知时，可以贴出题型、时长、分值和作答语言。再补充剩余的备考时间和已学内容，技能会据此安排复习顺序。

```text
用 ai-exam-prep 帮我准备腾讯算法工程师技术面试。我只有两晚，每晚一小时。请搜索公开面经，整理考点总表、项目追问和原创练习。
```

### 常用场景

| 你想做什么 | 可以这样问 |
| --- | --- |
| 了解岗位 | `用 ai-exam-prep 根据这份 JD，说明日常工作、主要产出和考核环节，再找公开经验帖。` |
| 从头准备笔试 | `用 ai-exam-prep 帮我准备软件测试工程师校招笔试。先给模块总表，标出考点、题型、掌握深度和出处，再带我学第一节。` |
| 同时准备多个岗位 | `用 ai-exam-prep 比较数据分析师和商业分析师的笔试，合并共通模块，标出各自需要单独补的考点。` |
| 按通知做模拟卷 | `用 ai-exam-prep 按我附上的笔试通知出一套原创模拟卷。沿用题型、时长和分值，单独给答案与解析。` |
| 练技术面或行为面 | `用 ai-exam-prep 根据公开面经和我提供的项目经历做模拟面试。一次问一题，等我答完再点评或追问。` |

在同一个聊天里可以接着说「继续下一节」「这一步为什么成立」「换一个条件再考我」或「把这一章整理成总结表」。需要留存时，可以要求把复习包保存为 Markdown 文件。

## 复习包怎么组织

| 部分 | 包含什么 |
| --- | --- |
| 考核概况 | 已知的招聘批次、环节、题型、时长和分值，以及待确认的信息。 |
| 模块总表 | 按模块、子主题和考点分层，逐项标注题型或面试轮次、掌握深度、复习优先级和来源。 |
| 学习计划 | 根据可用时间安排先学、再练和有余力再补的内容，并给出第一个可以立刻完成的任务。 |
| 笔试训练 | 标出每节在总表中的位置，解释解题依据和常见错误。按需加条件变式、章节小结或原创模拟卷。 |
| 面试训练 | 按可核实的轮次整理主问题、考查点、回答提纲和可能追问。有个人经历时，用真实素材准备口述。 |

### 来源怎么核对

技能先搜目标公司、团队和岗位，打开原帖核对招聘类型、批次和考核环节，再按缺少的模块或题型补搜。转载和汇总帖引用的同一经历只计一次。只能看到搜索摘要的材料会标明可见范围。

复习包会区分候选人的**历史回忆**、根据岗位描述得出的 **JD 推断**、**相近岗位参考**和**先修基础**。练习和模拟题会标为原创。本次考试安排以当期公告或你收到的通知为准。

## 常见问题

**公开经验帖太少怎么办？** 技能会标出证据缺口，并用相近岗位经验或 JD 补充基础复习，注明这些内容与目标岗位的关系。

**当前聊天无法使用网页搜索怎么办？** 可以贴上已有的经验帖正文、JD 或考试通知，继续做归类、排优先级和生成练习。

**怎么用自己的经历准备面试？** 给出一段真实项目或行为经历，尽量写清你负责的部分、采取的行动、实际结果和反思。需要补充的细节会留在回答提纲中。

**从哪里看完整示例？** 仓库里的腾讯算法工程师案例展示了如何从两篇公开面经整理复习总表、两晚学习计划、原创练习和项目口述题。[打开示例](examples/tencent-algorithm-engineer.md)
