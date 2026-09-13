# Project Context Memory

一个面向 Codex 的本地插件，用普通 Markdown 文件维护项目的长期认知，让工作可以跨对话、跨模型和跨编辑器继续。

## 它解决什么问题

对话结束后，模型通常不会保留完整的项目理解。这个插件把可迁移的认知写入项目本身，包括：

- 项目目标与范围
- 当前状态和系统结构
- 关键决策及原因
- 运行、兼容性和隐私约束
- 未决问题与假设
- 下一次交接的具体入口
- 已通过和未执行的验证

认知文件是普通 Markdown，不绑定某个模型或 Codex 数据库。把它和项目一起提交到 Git，就可以在另一台电脑、另一个 Codex 对话或其他支持 Agent Skills 的模型中继续。

## 安装

### Codex Desktop

1. 打开 **Settings → Plugins**。
2. 添加本仓库作为本地 Marketplace，或从仓库目录安装插件。
3. 安装并启用 **Project Context Memory**。
4. 重启 Codex，使新的 Skill 被发现。

### Codex CLI

将仓库作为本地 Marketplace 使用，或把 `skills/project-context-memory` 复制到 `~/.codex/skills/project-context-memory`。安装后重新启动 Codex。

### VS Code

使用与 CLI 相同的 Codex 配置目录。插件本身不依赖 VS Code API，因此无需额外的编辑器扩展。

## 第一次使用

在项目根目录打开 Codex，输入：

```text
使用 $project-context-memory，先扫描项目并创建或更新 PROJECT_CONTEXT.md。
只记录可以从仓库验证的事实，并列出当前未决问题和下一步交接。
```

如果项目已有 `.codex/project-context.md` 或 `docs/project-context.md`，插件会优先使用已有文件，不创建第二份竞争副本。

## 日常工作流

开始任务时：

```text
先读取项目认知文件和 Next handoff，再开始处理这个问题。
```

完成重要改动后：

```text
使用 $project-context-memory，更新本次变更影响的架构、决策、验证状态和下一步交接。
```

准备交给另一个对话或模型时：

```text
使用 $project-context-memory，整理一个可迁移的交接：当前状态、已验证事实、阻塞项、下一步动作和相关文件。
```

## 认知文件约定

默认文件名是 `PROJECT_CONTEXT.md`。建议保留以下章节：

1. Mission and scope
2. Current state
3. System map
4. Decisions
5. Constraints
6. Open questions
7. Next handoff
8. Verification

不要写入 API 密钥、访问令牌、私钥、隐藏推理过程或大段日志。对不确定内容使用 `Assumption`，对未验证内容使用 `Unverified`。

## 启用和关闭

在 Codex UI 的 **Settings → Plugins** 中切换 **Project Context Memory** 的开关。

CLI 单次关闭：

```powershell
codex -c 'plugins."project-context-memory@project-context-local".enabled=false'
```

永久关闭：把配置中的 `enabled = true` 改成 `enabled = false`。关闭插件不会删除项目中的认知文件。

## 跨模型迁移

把 `PROJECT_CONTEXT.md` 随项目提交或复制到新环境，然后在新对话中先要求模型读取它。模型不需要知道原始对话内容；只要能读取项目文件，就能从 `Current state` 和 `Next handoff` 继续。

## 设计边界

插件维护的是经过整理的项目事实和交接信息，不是完整聊天记录，也不会自动同步外部账号或云端记忆。它不会替用户决定未决事项；冲突时以当前用户指令和仓库代码为准，并修正认知文件。

## License

MIT
