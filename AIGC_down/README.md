# AIGC_down — 论文降重与AIGC痕迹修订 Skill

根据查重报告和AIGC检测报告，自动修改 Markdown 论文，提升原创性和自然学术表达。

## 支持平台

- **Trae**（及所有 Claude 系 IDE）
- **Claude Code**（终端 AI 编程助手）

## 文件结构

```
AIGC_down/
├── SKILL.md                  # 核心技能文件（Trae + Claude Code 通用）
├── claude-code-command.md    # Claude Code 专用斜杠命令文件
├── evals/
│   └── evals.json            # 评估测试用例
└── README.md                 # 本文件
```

---

## 安装方式

### 方式一：Trae / Claude 系 IDE（Skill 模式）

Skill 模式下，Claude 会根据对话内容**自动判断**何时调用此技能。

1. 将整个 `AIGC_down/` 文件夹复制到你的 Skill 存放目录：
   - **Trae**：将文件夹放入 Trae 的 Skills 目录
   - **Claude Desktop**：将文件夹放入 `~/.claude/skills/` 目录
2. 确保文件夹内包含 `SKILL.md` 文件
3. 重启 IDE，Skill 即可自动生效

### 方式二：Claude Code（斜杠命令模式）

斜杠命令模式下，你可以通过 `/project:aigc-down` **手动触发**。

1. 将 `claude-code-command.md` 文件复制到项目的 `.claude/commands/` 目录下，并重命名：
   ```
   .claude/commands/aigc-down.md
   ```
2. 如果想全局可用（所有项目），复制到：
   ```
   ~/.claude/commands/aigc-down.md
   ```
3. 在 Claude Code 中输入 `/project:aigc-down` 即可触发
4. 可选：在命令后追加自定义AIGC润色提示词，例如：
   ```
   /project:aigc-down 保持本科毕业论文语气，句子短一点，多保留工程实现细节
   ```

### 方式三：Claude Code（Skill 模式）

Skill 模式下，Claude Code 也会自动判断何时调用。

1. 将整个 `AIGC_down/` 文件夹复制到：
   - 项目级：`.claude/skills/AIGC_down/`
   - 全局级：`~/.claude/skills/AIGC_down/`
2. 确保 `SKILL.md` 在文件夹内
3. Claude Code 会自动识别并按需加载

---

## 使用方法

### 前置条件

1. 一个由 `thesis-writer` 生成的 Markdown 论文文件（`.md`）
2. 一个 `查重/` 文件夹，包含查重报告和/或 AIGC 检测报告
   - 支持格式：`.html`、`.pdf`、`.docx`、`.md`、`.txt`

### 触发方式

直接在对话中描述需求即可，例如：

- "请根据查重报告修改我的论文"
- "降低重复率，处理标红内容"
- "根据AIGC检测报告修改论文"
- "处理查重文件夹里的报告，改一下 thesis-writer 生成的论文"

### 自定义AIGC润色提示词

你可以提供自定义的AIGC段落润色提示词，例如：

> "保持本科毕业论文语气，句子短一点，多保留工程实现细节，不要新增结论"

如果不提供，将使用内置的默认学术化润色指导。

---

## 工作流程

1. **定位材料**：检查 `查重/` 文件夹，识别报告类型和论文文件
2. **构建修订映射**：标记需要修改的段落及约束条件
3. **处理高重复段落**：从关键点重构，逐段改写（每段不超过500字）
4. **处理AIGC标记段落**：应用学术化润色，使表达更自然
5. **生成修订文件**：输出新的 `.md` 文件，不覆盖原文件
6. **输出修订摘要**：报告修改内容和注意事项

## 安全与诚信

本 Skill 仅用于合法的原创性提升和来源规范的修订，**不承诺**通过任何检测系统，**不帮助**隐藏抄袭行为。
