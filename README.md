# 洛时Sera的小屋 1.0

MC 像素风的个人主页，深空蓝紫 + 星光黄，主题是「在方块与月亮之间」。

- 线上地址：<https://seraluoshi.github.io/>（需在 GitHub Pages 启用后生效）
- 源码仓库：<https://github.com/Sera-luoshi/seraluoshi.github.io>
- 技术栈：纯 HTML + CSS + 原生 JavaScript，单文件 `index.html`，无构建、无框架、无外部依赖

---

## 页面结构

| 区块 | 内容 |
| --- | --- |
| 首屏 | 像素小屋主视觉、状态栏、B 站 / 赞助 / 作品入口 |
| 滚动条 | 版本、粉丝群、二创、新项目等公告轮播 |
| 公告栏 `#notice` | 最新公告 + 可展开的历史公告 |
| 传送门 `#links` | B 站、爱发电、GitHub、邮箱 |
| 社区 `#feedback` | 粉丝群（筹备中）、内测群（暂未开放）、问题反馈 |
| 项目 `#projects` | 唱片大冒险、洛时的小屋 1.0、新模组 |
| 画册 `#gallery` | 个人设定 06 张 + 同人二创 04 张，支持灯箱翻页 |
| 底部 | 加入我们、页脚导航与版权 |

---

## 当前链接

| 用途 | 地址 |
| --- | --- |
| 哔哩哔哩 | <https://space.bilibili.com/105331722> |
| 爱发电 | <https://afdian.com/a/Achilles_Sera> |
| GitHub | <https://github.com/Sera-luoshi> |
| 邮箱 | [achillesseraluoshi@163.com](mailto:achillesseraluoshi@163.com) |
| 小屋源码 | <https://github.com/Sera-luoshi/seraluoshi.github.io> |

**社群状态**

- 粉丝群：还没建好，页面上标为「暂未开放」，按钮暂时指向 B 站。
- 内测群：暂未开放，进度先发在 B 站。
- 等群建好后，把页面上的「暂未开放」换成群号，并把按钮改成 QQ 加群链接即可，不要保留假的 `href`。

**项目说明**

- `唱片大冒险`：B 站连载的原创像素动画，链接指向 B 站投稿页。
- `洛时的小屋 1.0`：就是当前这个页面，源码链接指向本仓库。
- `新模组`：开发中，关注 B 站进度。

> 画册里的同人作者目前还是「待补充」，发布或转载前记得补上作者名并取得授权。

---

## 文件结构

```text
.
├─ index.html              页面本体（样式、脚本都在里面）
├─ README.md
└─ assets/
   ├─ avatar.png           首屏主视觉（正方形）
   ├─ favicon.png          浏览器标签图标
   ├─ projects/
   │  ├─ record.png        唱片大冒险 封面（16:9，960×540）
   │  ├─ cabin.png         小屋 1.0 预览（16:9）
   │  ├─ mystery.png       新模组 预览（16:9）
   │  └─ engine.png        旧占位图，目前未使用，可删
   ├─ artbook/
   │  └─ 01.png ~ 06.png   个人设定（4:5，600×750）
   └─ fanart/
      └─ 01.png ~ 04.png   同人二创（4:5，600×750）
```

---

## 修改指南

### 1. 改链接

直接搜索对应文字或 `href`：

- 首屏与卡片里的 B 站：`https://space.bilibili.com/105331722`
- 赞助：`https://afdian.com/a/Achilles_Sera`
- GitHub：`https://github.com/Sera-luoshi`
- 邮箱：`mailto:achillesseraluoshi@163.com`（两处：传送门卡片、页脚）

### 2. 换图片

保持文件名不变、直接覆盖最省事：

- 项目封面：`960×540`（16:9），文件名对应 `assets/projects/`
- 画册 / 二创：`600×750`（4:5），文件名对应 `assets/artbook/`、`assets/fanart/`
- 首屏：正方形，建议 `600×600` 以上

如果改了文件名，要同时改 `index.html` 里的 `src` 和灯箱用的 `data-full`。
想增加作品，复制一整段 `<button class="art-card">...</button>`，并更新标签上的数量。

### 3. 改配色

在 `index.html` 顶部的 `<style>` 里改 `:root`：

```css
--purple: #9b6dff;   /* 主紫 */
--blue:   #4d8dff;   /* 主蓝 */
--yellow: #ffd84d;   /* 星光黄 */
--bg:     #0a0720;   /* 深空背景 */
```

### 4. 发新公告

公告使用原生 `<details>`，不需要额外 JS。复制最新公告整段，改日期和正文，然后：

1. 新公告保留 `class="notice-item is-latest" open`，加上 `NEW` 标签。
2. 旧公告删掉 `is-latest`、`open` 和 `NEW`，移到「历史公告」下方。
3. 更新 `<span class="notice-count">03</span>` 里的数字。

日期显示建议 `2026.11.01`，`<time datetime="2026-11-01">` 里写标准格式。

---

## 发布到 GitHub Pages

1. 提交并推送最新代码：
   - 用 GitHub Desktop：`Commit to main` → `Push origin`
   - 或命令行：`git add -A && git commit -m "Update site" && git push`
2. 打开仓库 **Settings → Pages**：
   - **Source** 选 `Deploy from a branch`
   - **Branch** 选 `main`，目录选 `/ (root)`
   - 保存
3. 在 **Actions** 里等待 `pages build and deployment` 变绿。
4. 访问 <https://seraluoshi.github.io/>，强刷确认。

> 如果线上仍是 404：优先检查 Pages 的源分支/目录是否指向 `main / (root)`；
> 若 Source 选的是 `GitHub Actions`，仓库里又没有对应工作流，就不会有部署。

---

## 发布前检查

- [x] 邮箱链接已补 `mailto:`，页脚同步
- [x] 粉丝群 / 内测群改为「暂未开放」，移除了假群号和无效链接
- [x] 公告条、社区文案、底部 CTA 不再声称群已开放
- [x] 项目 1 改为 B 站动画《唱片大冒险》，链接和封面已对应
- [x] 全站版本号统一为 1.0，标题统一为「月亮」
- [x] 分享图改为绝对地址，补了 `og:url` 和 canonical
- [ ] 启用 GitHub Pages 并推送最新提交
- [ ] 图库作者名、同人授权
- [ ] 项目封面换成真实截图（目前是像素占位图）
- [ ] 手机再走一遍，确认没有横向滚动

---

## 本地预览

直接双击 `index.html`。
如果浏览器限制本地文件，可以在该目录执行：

```bash
python -m http.server 8000
```

然后访问 <http://localhost:8000>。
