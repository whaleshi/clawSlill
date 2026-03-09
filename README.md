# whale-share

在 [OpenClaw](https://openclaw.ai) 中通过 [Moltbook](https://www.moltbook.com) API 注册智能体并发帖的 Skill，面向 [ClawHub](https://clawhub.com) 安装与分发。

## 安装（ClawHub）

```bash
clawhub install @whaleshi/whale-share
```

安装后刷新 OpenClaw skills 或重启网关即可使用。

## 发布到 ClawHub

### 1. 安装 CLI

```bash
npm i -g clawhub
# 或
pnpm add -g clawhub
```

### 2. 登录

```bash
clawhub login
```

按提示在浏览器中完成登录（需 [clawhub.ai](https://clawhub.ai) 账号，GitHub 账号需满一周才能发布）。

### 3. 发布本 Skill

ClawHub CLI 在仓库含 `.git` 时可能报错（"Path must be a folder" 或 "SKILL.md required"），建议用**复制到临时目录再发布**：

```bash
# 在项目根目录执行（把 /path/to/clawSlill 换成你当前仓库路径）
cd /Users/shijy/Desktop/work/test

# 复制 skill 到临时目录（排除 .git）
rsync -av --exclude=.git --exclude=node_modules skills/whale-share/ /tmp/whale-share-pub/

# 发布
clawhub publish /tmp/whale-share-pub --slug whale-share --name "whale-share" --version 1.0.0 --tags latest
```

若你确定当前环境无此问题，也可直接：

```bash
cd skills/whale-share
clawhub publish . --slug whale-share --name "whale-share" --version 1.0.0 --tags latest
```

发布成功后，他人安装：`clawhub install @whaleshi/whale-share`。  
仓库：https://github.com/whaleshi/clawSlill

## 使用

在 OpenClaw 对话中提到「Moltbook」「发帖」「分享到 Moltbook」等，agent 会应用本 skill，指导：

1. 用 Moltbook API 或 `npx molthub register` 注册智能体  
2. 用 curl 按 `title` / `content` / `submolt` 发帖  
3. 可选：用环境变量保存 API Key  

## 在 Moltbook 发帖宣传本 Skill

注册并取得 API Key 后，可在 Moltbook 发一条介绍帖（建议 submolt：`agents` 或 `aitools`）。

**标题**

```
分享一个 OpenClaw skill：whale-share
```

**正文（可复制后微调）**

```markdown
给 OpenClaw 写了一个 **whale-share** skill，在对话里就能完成 Moltbook 注册智能体、用 API 发帖。

- 指导用 Moltbook API 或 `npx molthub register` 注册
- 按官方格式发帖（title / content / submolt）
- 支持用环境变量存 API Key

**安装：** ClawHub 安装 `clawhub install @whaleshi/whale-share`，刷新 skills 即可。

欢迎试用～
```

**curl 示例**

```bash
curl -X POST https://www.moltbook.com/api/v1/posts \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"title": "分享一个 OpenClaw skill：whale-share", "content": "（此处粘贴上面正文）", "submolt": "agents"}'
```

## 许可

MIT。发布到 ClawHub 时请保留来源说明。
