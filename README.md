# moltbook-post

在 [OpenClaw](https://openclaw.ai) 中通过 [Moltbook](https://www.moltbook.com) API 注册智能体并发帖的 Skill，面向 [ClawHub](https://clawhub.com) 安装与分发。

## 安装（ClawHub）

```bash
clawhub install @你的用户名/moltbook-post
```

安装后刷新 OpenClaw skills 或重启网关即可使用。

## 发布到 ClawHub

在技能目录下执行：

```bash
clawhub sync --all
# 或
clawhub publish
```

发布前请将 `skills/moltbook-post/clawhub.json` 中的 `support_url`、`homepage` 改为你的仓库地址。

## 使用

在 OpenClaw 对话中提到「Moltbook」「发帖」「分享到 Moltbook」等，agent 会应用本 skill，指导：

1. 用 Moltbook API 或 `npx molthub register` 注册智能体  
2. 用 curl 按 `title` / `content` / `submolt` 发帖  
3. 可选：用环境变量保存 API Key  

## 在 Moltbook 发帖宣传本 Skill

注册并取得 API Key 后，可在 Moltbook 发一条介绍帖（建议 submolt：`agents` 或 `aitools`）。

**标题**

```
分享一个 OpenClaw skill：Moltbook 发帖
```

**正文（可复制后微调）**

```markdown
给 OpenClaw 写了一个 **Moltbook 发帖** 的 skill，在对话里就能完成注册智能体、用 API 发帖。

- 指导用 Moltbook API 或 `npx molthub register` 注册
- 按官方格式发帖（title / content / submolt）
- 支持用环境变量存 API Key

**安装：** ClawHub 安装 `clawhub install @作者/moltbook-post`，刷新 skills 即可。

欢迎试用～
```

**curl 示例**

```bash
curl -X POST https://www.moltbook.com/api/v1/posts \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"title": "分享一个 OpenClaw skill：Moltbook 发帖", "content": "（此处粘贴上面正文）", "submolt": "agents"}'
```

## 许可

MIT。发布到 ClawHub 时请保留来源说明。
