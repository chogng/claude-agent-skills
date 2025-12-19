# Claude Agent Skills

Custom skills for Claude Code CLI. 为 Claude Code 命令行工具定制的技能扩展包。

---

## Skills 列表

### git-release

Git 项目版本发布自动化工具，基于语义化版本 (Semantic Versioning) 和 Angular Commit 规范。

#### 功能特性

| 功能 | 描述 |
|-----|------|
| 版本号管理 | 自动计算并更新 `package.json` 中的版本号 |
| 语义化版本 | 支持 major（大版本）、minor（小版本）、patch（补丁）三种升级类型 |
| CHANGELOG 生成 | 基于 Git commits 自动生成更新日志 |
| Git Tag 创建 | 自动创建版本标签 `vX.Y.Z` |
| 远程推送 | 一键推送 commits 和 tags 到远程仓库 |

#### 版本类型说明

| 类型 | 何时使用 | 版本变化示例 |
|-----|---------|-------------|
| **patch** | Bug 修复、文档更新、小改动 | `1.2.3` → `1.2.4` |
| **minor** | 新增功能、向后兼容的改进 | `1.2.3` → `1.3.0` |
| **major** | 破坏性变更、API 重构、不兼容更新 | `1.2.3` → `2.0.0` |

#### 触发关键词

Claude 会在你说以下内容时自动触发此 skill：

**中文关键词：**
- 发布版本、升级版本、更新版本、版本发布、发新版
- 更新版本并提交、升级并提交、发布并推送
- 大版本更新、小版本更新、补丁版本
- 打 tag、创建发布、创建 tag

**英文关键词：**
- bump version、release、new release
- major release、minor release、patch release

**快捷表达：**
- "大更新" / "大版本" → 自动识别为 major
- "小更新" / "小版本" / "新功能" → 自动识别为 minor
- "修复" / "补丁" / "bugfix" / "hotfix" → 自动识别为 patch

#### 工作流程

```
1. 检查前置条件
   ├── 确认工作区状态（是否有未提交更改）
   ├── 确认当前分支
   └── 获取当前版本号和最新 tag

2. 询问版本类型
   └── patch / minor / major（除非用户已明确指定）

3. 处理未提交更改（如有）
   ├── 先提交再发布（推荐）
   ├── 先 stash 再发布
   └── 取消发布

4. 更新版本号
   └── 修改 package.json 中的 version 字段

5. 生成 CHANGELOG
   └── 按 Angular 规范分组 commits

6. 提交发布
   ├── git add package.json CHANGELOG.md
   ├── git commit -m "chore(release): vX.Y.Z"
   └── git tag -a vX.Y.Z -m "Release vX.Y.Z"

7. 推送到远程（询问确认后）
   ├── git push origin <branch>
   └── git push origin vX.Y.Z
```

#### 使用示例

```
用户: 帮我发布一个新版本
Claude: [检查项目状态，询问版本类型，执行发布流程]

用户: 小版本更新
Claude: [自动识别为 minor，执行 1.2.3 → 1.3.0]

用户: 修复了一个 bug，更新版本并提交
Claude: [自动识别为 patch，执行 1.2.3 → 1.2.4]

用户: major release
Claude: [执行大版本升级 1.2.3 → 2.0.0]
```

#### 包含文件

```
git-release/
├── SKILL.md                      # 主指令文件（Claude 读取的核心文件）
├── scripts/
│   └── bump-version.sh           # 版本号升级脚本
├── references/
│   ├── angular-commit.md         # Angular Commit 规范参考
│   └── semver-guide.md           # 语义化版本指南
└── assets/
    └── CHANGELOG.template.md     # CHANGELOG 模板
```

#### Commit 规范

此 skill 遵循 Angular Commit 规范：

```
<type>(<scope>): <subject>

类型 (type):
- feat:     新功能
- fix:      Bug 修复
- docs:     文档变更
- style:    代码格式
- refactor: 重构
- perf:     性能优化
- test:     测试相关
- chore:    其他杂项
```

---

## 安装方法

### macOS / Linux

```bash
# 克隆仓库
git clone https://github.com/chogng/claude-agent-skills.git

# 复制 skill 到 Claude skills 目录
cp -r claude-agent-skills/git-release ~/.claude/skills/
```

### Windows

```powershell
# 克隆仓库
git clone https://github.com/chogng/claude-agent-skills.git

# 复制 skill 到 Claude skills 目录
xcopy /E /I claude-agent-skills\git-release %USERPROFILE%\.claude\skills\git-release
```

---

## 目录结构

```
claude-agent-skills/
├── README.md                 # 本文件
├── git-release.skill         # 打包好的 skill 文件（zip 格式）
└── git-release/              # Skill 源文件目录
    ├── SKILL.md
    ├── scripts/
    ├── references/
    └── assets/
```

---

## License

MIT
