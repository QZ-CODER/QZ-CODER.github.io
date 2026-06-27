---
title: 博客操作流程指南（本地草稿）
date: 2026-06-27 18:00:00
tags:
  - 指南
categories:
  - 杂记
---

> 这是一篇**草稿**，放在 `source/_drafts/` 目录下。
> 它只在本地 `hexo server --draft` 时可见，**不会**被 GitHub Actions 构建到线上。

## 一、整体原理

```
写 .md 文件  →  push 到 source 分支  →  GitHub Actions 自动构建  →  网站更新
   (你做)        (你做)                  (自动)                  (自动)
```

你只需要做两件事：**①写 md 文件 ②push**。其余全自动。

## 二、写一篇正式文章（会发布到线上）

```bash
# 1. 切到 source 分支（源码在这里）
git checkout source

# 2. 生成文章文件（会出现在 source/_posts/ 下）
npx hexo new "文章标题"

# 3. 编辑 source/_posts/文章标题.md，在 --- 下面用 Markdown 写正文

# 4. 推送上线
git add -A
git commit -m "发布：文章标题"
git push
```

push 后等 1～2 分钟，<https://qz-coder.github.io> 自动更新。

## 三、写草稿（只本地可见，不发布）

```bash
# 1. 生成草稿（出现在 source/_drafts/ 下，而不是 _posts/）
npx hexo new draft "草稿标题"

# 2. 本地预览（带 --draft 才能看到草稿）
npx hexo server --draft
# 打开 http://localhost:4000 查看
```

草稿写好后若想正式发布，把它从 `_drafts/` 移到 `_posts/`：

```bash
npx hexo publish "草稿标题"
# 然后 git add / commit / push 上线
```

## 四、本地实时预览

```bash
npx hexo clean          # 清缓存（出问题时用）
npx hexo server         # 普通预览，http://localhost:4000
npx hexo server --draft # 连草稿一起预览
```

改动 md 文件后浏览器会自动刷新，所见即所得。

## 五、常用命令速查

| 命令 | 作用 |
| --- | --- |
| `npx hexo new "标题"` | 新建正式文章（_posts/） |
| `npx hexo new draft "标题"` | 新建草稿（_drafts/） |
| `npx hexo publish "标题"` | 草稿转正式 |
| `npx hexo server` | 本地预览 |
| `npx hexo server --draft` | 本地预览（含草稿） |
| `npx hexo clean` | 清理缓存 |
| `git add -A && git commit -m "..." && git push` | 提交上线 |

> 注意：`hexo generate`（生成线上 HTML）已交给 GitHub Actions 自动完成，本地一般不需要手动跑。
