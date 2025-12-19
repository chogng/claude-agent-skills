# Claude Agent Skills

Custom skills for Claude Code CLI.

## Available Skills

### git-release

Git 项目版本发布自动化工具。

**功能：**
- 语义化版本号升级 (major/minor/patch)
- 自动生成 CHANGELOG
- 创建 Git tag 并推送

**触发关键词：**
- 发布版本、升级版本、更新版本
- bump version、release
- 大版本更新、小版本更新

**安装：**
```bash
# 复制 skill 文件夹到 Claude skills 目录
cp -r git-release ~/.claude/skills/
```

## 目录结构

```
├── git-release/          # Skill 源文件
│   ├── SKILL.md          # 主指令文件
│   ├── scripts/          # 自动化脚本
│   ├── references/       # 参考文档
│   └── assets/           # 模板文件
└── git-release.skill     # 打包好的 skill 文件
```

## License

MIT
