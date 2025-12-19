# Claude Agent Skills

为 Claude Code 命令行工具定制的技能扩展包。

Custom skills for Claude Code CLI.

## Skills 列表

| Skill | 描述 | 状态 |
|-------|------|------|
| [git-release](./git-release/) | Git 版本发布自动化（语义化版本、CHANGELOG、Tag） | ✅ 可用 |

## 快速安装

### 安装单个 Skill

```bash
# macOS / Linux
cp -r <skill-name> ~/.claude/skills/

# Windows
xcopy /E /I <skill-name> %USERPROFILE%\.claude\skills\<skill-name>
```

### 安装全部 Skills

```bash
# macOS / Linux
git clone https://github.com/chogng/claude-agent-skills.git
for skill in git-release; do
  cp -r "claude-agent-skills/$skill" ~/.claude/skills/
done

# Windows PowerShell
git clone https://github.com/chogng/claude-agent-skills.git
$skills = @("git-release")
foreach ($skill in $skills) {
  Copy-Item -Recurse "claude-agent-skills\$skill" "$env:USERPROFILE\.claude\skills\$skill"
}
```

## 目录结构

```
claude-agent-skills/
├── README.md                 # 本文件（索引页）
├── git-release/              # git-release skill
│   ├── README.md             # skill 详细文档
│   ├── git-release.skill     # 打包文件
│   ├── SKILL.md              # 主指令文件
│   ├── scripts/              # 脚本
│   ├── references/           # 参考文档
│   └── assets/               # 模板资源
└── <future-skill>/           # 未来更多 skills...
```

## 贡献

欢迎提交 Pull Request 添加新的 skill！

每个 skill 目录应包含：
- `README.md` - skill 详细说明
- `SKILL.md` - Claude 读取的主指令文件
- `<skill-name>.skill` - 打包后的文件（可选）
- `scripts/` / `references/` / `assets/` - 资源文件（按需）

## License

MIT
