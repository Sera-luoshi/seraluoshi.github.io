# 洛时Sera的小屋 2.0 · 使用说明

一个单文件 + 图片素材的静态个人主页，MC 像素风，主色为深空蓝紫 + 星光黄。
不需要安装任何依赖，双击 `index.html` 就能在浏览器里打开。

---

## 一、需要你替换的占位内容

页面里所有需要改的地方都写了 `TODO` 注释，用编辑器搜索 `TODO` 就能逐个定位。

| 位置 | 现在的内容 | 要改成 |
| --- | --- | --- |
| 首屏「去 B 站找我」 | 已填你的 B 站主页 `space.bilibili.com/105331722` | 如需换号再改 |
| 链接区「哔哩哔哩」 | 同上 | — |
| 链接区「赞助小屋」 | `href="#"` | 爱发电 / 面包多 / Ko-fi 等赞助页 |
| 链接区「GitHub」 | `href="#"` | 你的 GitHub 主页 |
| 链接区「写封邮件」 | `mailto:hello@example.com` | 你的邮箱 |
| 粉丝群卡片的群号 | `123 456 789` / `data-copy="123456789"` | 真实群号（两处一起改） |
| 内测群卡片的群号 | `987 654 321` / `data-copy="987654321"` | 真实群号（两处一起改） |
| 两个「申请加入 / 申请内测」按钮 | `href="#"` |  QQ 加群链接，例如 `https://qm.qq.com/q/xxxxxx` |
| 反馈邮箱 | `hello@example.com` | 你的反馈邮箱（文本、`data-copy`、`mailto:` 三处） |
| 项目卡片 | 示例项目 Sera Engine / 小屋 2.0 / 未公开新作 | 换成你的真实项目和链接 |
| 同人作品作者 | `by 待补充` | 画师名字（记得取得授权） |

> 群号显示带空格只是为了好看，`data-copy` 里要写不带空格的纯数字，复制按钮复制的就是它。

---

## 二、替换图片

所有图片都在 `assets/` 下，**保持文件名不变直接覆盖**最省事：

```
assets/
├─ avatar.png            首屏头像 / 主视觉（正方形，建议 600×600 以上）
├─ favicon.png           浏览器标签图标（建议 64×64）
├─ projects/
│  ├─ engine.png         项目 01 预览图（16:9，建议 960×540）
│  ├─ cabin.png          项目 02 预览图
│  └─ mystery.png        项目 03 预览图
├─ artbook/
│  ├─ 01.png ~ 06.png    个人设定画册（4:5，建议 600×750）
└─ fanart/
   ├─ 01.png ~ 04.png    粉丝同人二创（4:5，建议 600×750）
```

- 图片会被 `image-rendering: pixelated` 处理，像素画放大不会糊，普通插画也能正常显示。
- 如果换了文件名，记得同时改 `index.html` 里的 `src` 和灯箱用的 `data-full`。
- 想加更多作品：复制一整段 `<button class="art-card" ...> ... </button>`，改标题、说明和图片路径；
  同时把标签上的数字 `06` / `04` 改成实际数量。

---

## 三、改颜色 / 字体

打开 `index.html`，最上面的 `<style>` 里有 `:root` 变量：

```css
--purple:#9b6dff;   /* 主紫 */
--blue:#4d8dff;     /* 主蓝 */
--yellow:#ffd84d;   /* 星光黄 */
--bg:#0a0720;       /* 深空背景 */
```

改这几个值，整站配色会一起变。

字体优先使用本机的像素字体 `Zpix` / `Fusion Pixel` / `Ark Pixel`，没有就回退到微软雅黑；
正文小字使用系统黑体以保证可读性，标题和界面文案保留像素感。

---

## 四、已经做好的交互

- 顶部导航：滚动时吸顶、当前区块高亮、手机端折叠菜单
- 群号 / 邮箱一键复制 + 提示条
- 画册「个人设定 / 粉丝二创」切换
- 点击作品打开灯箱：左右箭头、键盘 ← →、Esc 关闭、手机滑动切换
- 滚动进入动画、回到顶部按钮（均尊重「减少动态效果」系统设置）
- 手机 / 平板 / 桌面响应式布局

---

## 五、本地预览

直接双击 `index.html` 即可。
如果浏览器限制本地文件，可以在该文件夹执行：

```bash
python -m http.server 8000
```

然后访问 `http://localhost:8000`。

---

## 六、上线前检查

- [ ] 所有 `TODO` 都替换完，`href="#"` 不再残留
- [ ] 群号、邮箱、QQ 加群链接正确
- [ ] 图片换成自己的作品，并压缩过体积
- [ ] 手机上看一遍，确认没有横向滚动
- [ ] 同人作品已获得作者授权并署名

以后怎么发新公告
复制正在用的「最新公告」整段 <details>...</details>。
改里面的日期、标题、正文。
把原来那条最新公告降级成历史：
删掉 is-latest
删掉 open（让它默认收起）
删掉 <span class="notice-tag">NEW</span> 这一行
把它剪切到 历史公告 那一行下面的最上面
把新的公告放到 历史公告 那一行上面，保留 class="notice-item is-latest" open 和 NEW。
把 <span class="notice-count">03</span> 里的数字加 1，变成历史公告的总数。
新公告模板（直接改日期和文字）：
<details class="notice-item is-latest" open>
  <summary>
    <span class="notice-date"><time datetime="2026-11-01">2026.11.01</time></span>
    <span class="notice-title">这里写公告标题</span>
    <span class="notice-tag">NEW</span>
    <span class="notice-toggle" aria-hidden="true"></span>
  </summary>
  <div class="notice-body">
    <p>第一段……</p>
    <p>第二段……</p>
  </div>
</details>
几个小提示：

日期显示格式随意，建议统一用 2026.11.01；datetime 里写标准格式 2026-11-01。
正文想分段就多写几个 <p>，会自动留间距。
公告里要放链接，用 <a href="https://..." target="_blank" rel="noopener noreferrer">文字</a>，会自动变成黄色。
不想让最新公告默认展开，把最新那条的 open 删掉即可。
公告特别长也没关系，正文会自动换行；手机端标题会换到日期下面一行。