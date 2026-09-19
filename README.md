# Cheng+RaccoonIngot Life Notes

一个简约的人文科技风日常生活记录站。主色调是 `#8A2B27`，当前版本是无依赖静态站点，可以直接由 Cloudflare Pages 托管。

## 结构

- `dist/index.html`：当前完整页面，包含样式和少量筛选交互。
- `.openai/hosting.json`：静态托管配置，输出目录为 `dist`。

## 当前交互

- 标签筛选：按 `日常`、`阅读`、`城市`、`灵感` 等标签过滤。
- 搜索：点击顶部搜索按钮，可搜索标题、摘要、地点、心情和标签。
- 详情面板：点击任意记录卡片，会打开记录详情。
- 快捷关闭：详情面板和搜索框支持 `Esc` 关闭。
- 自动统计：记录数、照片数、标签数和本月进度会根据 `records.json` 自动计算。

## 日常更新

现在记录源文件在 `content/records/*.md`，发布用数据在 `dist/data/records.json`。

日常建议：让 Hermes 或你自己继续写 Markdown；发布前把 Markdown 转成 `records.json`。

字段说明：

```json
{
  "title": "晚饭后散步",
  "date": "2026-09-19",
  "weekday": "Saturday",
  "tags": ["日常", "散步"],
  "mood": "平静",
  "location": "上海",
  "photos": 2,
  "summary": "路灯亮得很早，风里有一点雨后的味道。"
}
```

注意：

- `date` 使用 `YYYY-MM-DD`。
- `tags` 用中文数组，建议恰好两枚：一级标签 + 二级标签。
- `photos` 是这条记录包含的照片数量，页面会自动统计。
- 更新后重新发布 Cloudflare Pages，朋友就能看到新版。

## 后续升级建议

如果记录变多，下一阶段建议迁移为：

```text
content/
  records/
    2026-09-19-walk.md
    2026-09-18-reading.md
public/
  images/
```

## Cloudflare Pages 发布和绑定域名

推荐做法：

1. 把整个项目上传到 GitHub。
2. 打开 Cloudflare Dashboard。
3. 进入 `Workers & Pages`。
4. 选择 `Create application`。
5. 选择 `Pages`，连接你的 GitHub 仓库。
6. 构建设置：
   - Framework preset: `None`
   - Build command: 留空
   - Build output directory: `dist`
7. 部署完成后，Cloudflare 会给一个 `*.pages.dev` 地址。
8. 在 Pages 项目里进入 `Custom domains`。
9. 添加你的域名，例如 `yourdomain.com` 或 `www.yourdomain.com`。
10. 如果域名 DNS 已经在 Cloudflare，按提示确认即可；如果域名不在 Cloudflare，需要先把 nameserver 指向 Cloudflare。

更新网站时：

1. 新增或修改 `content/records/*.md`。
2. 更新 `dist/data/records.json`。
3. 提交并推送到 GitHub。
4. Cloudflare Pages 会自动重新部署。

记录格式建议：

```yaml
---
title: 晚饭后散步
date: 2026-09-19
tags: [日常, 散步]
mood: 平静
location: 上海
cover:
---

路灯亮得很早，风里有一点雨后的味道。
```

## 给 Hermes 的并行任务

```text
你负责为一个个人日常生活记录网站准备可批量导入的内容素材，不要修改网站代码。

项目风格：简约、科技感和人文风并存；主色 #8A2B27；布局参考轻量后台/工作台式 UI，内容是个人生活记录。

请输出以下内容：
1. 设计一个长期可用的标签体系，分为一级标签和二级标签，控制在 30 个以内。
2. 生成 30 条真实感生活记录样例，每条包含 title、date、tags、mood、location、summary、body。
3. 日期范围覆盖最近 45 天，内容包括日常、阅读、饮食、散步、城市、灵感、整理、朋友、电影、工作后的生活。
4. body 用中文，避免鸡汤，保持具体、克制、有人味，每条 80-180 字。
5. 输出为 Markdown 文件建议清单：文件名、frontmatter、正文。
6. 最后检查：日期格式统一为 YYYY-MM-DD；tags 必须来自你设计的标签体系；每条都要适合放到公开个人网站。

不要做技术选型，不要生成前端代码，不要讨论部署，只做内容素材和字段规范。
```
