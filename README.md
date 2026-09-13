# plan-first：先议后行

一个 AI 协作机制 skill：任何会产生变更的任务，先出方案、等用户确认后才执行（议行分离）。适用于 Claude Code / DeepSeek Harness / ZCode 等支持 skills 机制的 Agent。

## 解决什么问题

AI 拿到任务就闷头改，改完才发现方向不对。plan-first 把「讨论方案」和「动手执行」强制分开：**方案未获确认，不产生任何持久影响**——不改文件、不跑有副作用的命令、不 push、不发布。

## 工作流程

1. **判定级别**：A 只读（直接做）/ B 小事（一句话确认）/ C 常规（完整方案块）/ D 复杂（方案块 + 阶段确认点）
2. **输出方案块**（C/D 类）：目标、方案选项与取舍、影响范围（含是否触及红线）、验证方式、待确认点
3. **等确认**：用户说「执行 / OK / 动手」才开工；收到修改意见则更新方案再来一轮
4. **执行纪律**：TodoWrite 建清单、逐项执行逐项验证、被阻塞就停下问、不自动 commit/push
5. **阶段确认**（仅 D 类）：一次批准只覆盖到下一个确认点

红线动作（删除文件 / git push / 改密钥 / 装全局依赖 / 对外发布）即使方案已确认，仍单独再问一次。

## 安装

把 `SKILL.md` 放进对应 Agent 的 skills 目录即可，无需其他文件：

| Agent | 目录 | 触发方式 |
|---|---|---|
| Claude Code | `~/.claude/skills/plan-first/` | `/plan-first` 或触发词 |
| DeepSeek Harness | `~/.dsh/skills/plan-first/` | `/plan-first` 或触发词 |
| ZCode | `~/.zcode/skills/plan-first/` | `$` 菜单或触发词（skills 不进 `/` 菜单） |

触发词：「先议后行」「先商量」「方案先行」「议行分离」「先出方案」「plan first」。

## 三侧差异

三侧正文一字不改；仅 frontmatter `description` 的触发措辞按侧适配（ZC 侧无 `/` 命令，写为「用户主动调用时直接运行」）。本仓库以 CC/DSH 版为准。

## 同系列 skill

- [agenttime](https://github.com/hongshuxifan321/agenttime)——会话回顾散文
- [econ-cn-docx](https://github.com/hongshuxifan321/econ-cn-docx)——经管论文中文排版
