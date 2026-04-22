# Qiaomu Blog Open Source

如果你也想拥有一个真正属于自己的学习、写作、分享阵地，而不是把内容完全寄托在平台算法上，这个项目就是为此做的。

Qiaomu Blog Open Source 是一个基于 Cloudflare Workers + OpenNext + Next.js 16 + D1 + R2 的开源博客系统。它不是一个只会渲染 Markdown 的静态模板，而是一套完整的写作、编辑、发布、搜索、AI 辅助内容生产系统。

默认只要求 `D1 + R2`，`KV / Queues / Workers AI / Vectorize / 图片增强` 都是可选增强能力。

这个仓库适合直接 `Use this template` 或 `fork` 后部署成你自己的博客。

## 为什么做这个项目

做这个系统的出发点很简单：

- 自媒体账号可能被封，平台流量可能波动，但自己的站点不会
- 有价值的内容，不应该只能依赖平台分发
- 写作和发布的阻力应该足够低，低到你随时都愿意更新

所以这个项目追求的不是“又一个博客模板”，而是：

- 像飞书、Notion 一样顺手的编辑体验
- 像自己的产品后台一样可控的配置能力
- 像现代 AI 工作流一样把琐事自动化
- 像 Cloudflare 这样的基础设施一样足够轻，维护成本足够低

## 这个项目解决什么问题

和传统博客系统相比，这个项目重点解决的是“内容生产和发布成本”：

- 打开就能写，不用在前后台之间反复切换心智
- 前台和后台都可以编辑，减少流程摩擦
- AI 自动处理标签、摘要、slug、封面这些重复劳动
- 多套主题直接可用，移动端阅读体验也一起考虑好了
- 完全部署在 Cloudflare，通常不需要自己买服务器和 CDN
- 可以继续接入你自己的外部工作流，比如 Obsidian、API Token、浏览器剪藏发布

## 核心体验

- 所见即所得编辑器：基于 Novel / Tiptap，目标是接近飞书和 Notion 的使用感
- 富内容粘贴：图片、音频、视频、PDF、Epub 等常见内容可以直接进入编辑流
- Ask AI / Bubble Menu：选中文本后就能直接改写、润色、扩写、翻译
- AI 发布辅助：自动生成摘要、标签、SEO 友好的 URL、封面图
- 生图工作流：支持多模型配置、快捷模版、历史记录检索、插入与替换
- 图片右键能力：下载、设为封面、对齐、裁剪、参考生图
- 多状态发布：公开、草稿、密码访问、链接访问
- 后台配置完整：导航、分类、主题、字体、自定义代码、API Token、模型配置都能管

## 适合谁

- 想搭建个人博客、知识库博客、AI 内容博客的人
- 想要“能长期写下去”的写作系统，而不是只搭个展示页的人
- 想把 AI 真正接进写作和发布流程的人
- 想基于 Cloudflare 部署，尽量降低维护成本的人

## 在线查看

- 线上博客：<https://blog.qiaomu.ai/>
- 介绍文章：<https://blog.qiaomu.ai/qiaomu-blog-opensource>
- 当前开源仓库：<https://github.com/joeseesun/qiaomu-blog-opensource>

## 作者

- 向阳乔木
- GitHub：<https://github.com/joeseesun>
- X / Twitter：<https://x.com/vista8>
- Blog：<https://blog.qiaomu.ai/>

## 内置能力

- Novel / Tiptap 可视化编辑器
- D1 + SQLite FTS5 全文搜索
- Cloudflare Workers 边缘部署
- 4 套首页主题：默认、精致极简、杂志编辑、AI 终端
- 后台可切换主题和正文字体
- 内置 AI 文本供应商预设
- 内置 AI 生图供应商预设
- 内置摘要、标签、slug、封面生成器

AI 相关预设不会携带任何 API Key。首次进入后台设置页时会自动初始化到数据库。

## 和普通博客模板的差别

- 不是只负责展示文章，也负责降低“写文章”这件事本身的摩擦
- 不是只给你一套主题，而是给你完整的后台、编辑器、AI 配置和发布能力
- 不是只适合程序员写 Markdown，也适合更接近飞书式的日常写作
- 不是把 AI 当噱头，而是把它放在真正有价值的环节上

## 技术栈

- Next.js 16
- React 19
- TypeScript
- OpenNext for Cloudflare
- Cloudflare D1
- Cloudflare R2
- Novel / Tiptap

## 快速开始

### 1. 创建你自己的仓库

- 直接点击 GitHub 上的 `Use this template`
- 或克隆本仓库：

```bash
git clone https://github.com/joeseesun/qiaomu-blog-opensource.git
cd qiaomu-blog-opensource
npm install
```

### 2. 配置本地环境变量

```bash
cp .env.example .env.local
```

最少需要：

```env
ADMIN_PASSWORD=change-me
ADMIN_TOKEN_SALT=change-me-to-a-random-string
AI_CONFIG_ENCRYPTION_SECRET=change-me-to-another-random-string
NEXT_PUBLIC_SITE_URL=http://localhost:3000
```

### 3. 本地开发

```bash
npm run dev
```

常用入口：

- 首页：`/`
- 后台：`/admin`
- 编辑器：`/editor`

如果你要用 Worker 运行时本地预览：

```bash
npm run preview
```

## 初始化 Cloudflare

先登录：

```bash
npx wrangler login
```

然后执行：

```bash
npm run cf:init -- --site-url=https://your-domain.com
```

如果你还要创建公共缓存 KV：

```bash
npm run cf:init -- --site-url=https://your-domain.com --with-kv
```

`npm run cf:init` 会自动：

1. 从模板 `wrangler.toml` 复制出本地 `wrangler.local.toml`
2. 创建 D1 数据库
3. 创建 R2 bucket
4. 可选创建 KV namespace
5. 写入真实 Cloudflare 绑定
6. 执行 `db/schema.sql`
7. 执行 `db/seed-template.sql`

初始化后，默认主题、默认字体和默认导航会直接可用。

## 部署

先设置 secrets：

```bash
npx wrangler secret put ADMIN_PASSWORD -c wrangler.local.toml
npx wrangler secret put ADMIN_TOKEN_SALT -c wrangler.local.toml
npx wrangler secret put AI_CONFIG_ENCRYPTION_SECRET -c wrangler.local.toml
```

如果你要启用外部 AI：

```bash
npx wrangler secret put AI_API_KEY -c wrangler.local.toml
```

然后：

```bash
npm run cf-typegen
npm run build
npm run deploy
```

当前链路是 OpenNext + Cloudflare Workers，不是 Cloudflare Pages。

## 资源要求

必需：

- `D1`
- `R2`

可选：

- `KV`
- `Queues`
- `Workers AI`
- `Vectorize`

## 常用命令

| 命令 | 说明 |
| --- | --- |
| `npm run dev` | Next.js 本地开发 |
| `npm run preview` | Worker 运行时本地预览 |
| `npm run build` | Next.js 构建 |
| `npm run verify:quick` | lint + test + build |
| `npm run verify` | 完整校验，额外包含 OpenNext build |
| `npm run cf:init` | 初始化 Cloudflare 资源和模板默认设置 |
| `npm run cf-typegen` | 生成 Cloudflare 类型 |
| `npm run deploy` | 部署到 Cloudflare Workers |

## 模板约定

- 提交到 Git 的 `wrangler.toml` 永远只放模板配置
- 真实资源绑定写进本地 `wrangler.local.toml`
- 仓库不包含任何私有资源 ID、私有域名、私有 API Key
- AI 功能默认可关闭，不会阻塞博客的写作、发布、搜索和展示

## License

MIT
