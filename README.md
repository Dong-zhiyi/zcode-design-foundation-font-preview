# 字体样张页 · design-foundation

一个自包含的静态页面，用来在浏览器里**预览和对比 design-foundation 的 13 个候选字体**，帮你在动手做设计之前把字体定下来。

- **在线地址（GitHub Pages）**：https://dong-zhiyi.github.io/zcode-design-foundation-font-preview/
- **所属项目**：design-foundation（设计基座）· 平台 / 技术栈 / 风格 / 架构 / 字体 / 图标的选型工作流
- **插件集成**：ZCode 插件 `design-foundation` 的配置项 `font_preview_url` 填上面那个地址即可

> 页面是单文件的：内联 CSS 与 JS，无构建步骤，`index.html` 与 `fonts/` 一起部署即可。
> 唯一的外链是 8 个拉丁字体走 CDN（见下方[字体清单](#字体清单与授权)）。

---

## 目录结构

```
zcode-design-foundation-font-preview/
├── index.html                                  # 页面本体（内联 CSS/JS）
├── README.md                                   # 本文件
└── fonts/
    ├── AlibabaPuHuiTi-3-45-Light.woff2         # 5.4 MB   Light（300）
    ├── AlibabaPuHuiTi-3-55-Regular.woff2       # 5.3 MB   Regular（400）
    ├── AlibabaPuHuiTi-3-65-Medium.woff2        # 5.5 MB   Medium（500）
    ├── AlibabaPuHuiTi-3-75-SemiBold.woff2      # 5.5 MB   SemiBold（600 / 700）
    ├── NotoSansSC-VF.ttf                       # 17.8 MB  思源黑体
    └── NotoSerifSC-VF.ttf                      # 25.1 MB  思源宋体
```

---

## 快速开始

### 本地预览

**方式一：直接双击 `index.html`** —— 页面能正常打开，布局、对比网格、样张都能看。
唯一差别是字体：多数浏览器会拦截 `file://` 下的字体加载（原因见下方[常见问题](#常见问题)），此时中文字体回退到系统字体。

**方式二：起个本地服务（推荐，能看到真实字形）**

在本目录执行：

```bash
# Python
python -m http.server 8731

# Node
npx -y serve -l 8731 .
```

然后打开 `http://127.0.0.1:8731/index.html`。

### 部署到服务器

把 `index.html` 和 `fonts/` **放在同一目录**上传即可（页面用相对路径 `./fonts/...` 加载字体）。

- **Nginx / OSS / COS / GitHub Pages / Vercel / Netlify**：直接上传，无需配置
- 访问地址形如 `https://你的域名/zcode-design-foundation-font-preview/`

**GitHub Pages**：仓库 Settings → Pages → Source 选 `Deploy from a branch` → 分支 `main` / 目录 `/ (root)` → Save。

---

## 页面功能

| 功能 | 说明 |
|---|---|
| 快速对比网格 | 所有字体同屏渲染同一段文案，字号可拖动调节 |
| 详细样张 | 每个字体单独一张卡片：大标题 / 标题 / 正文 / 辅助文字 / 英文数字 / 4 档字重对比 |
| 自定义文案 | 顶部输入框，输入你的真实文案（比如「歌剧《图兰朵》」）看实际效果 |
| 类型筛选 | 全部 / 中文 / 英文 / 等宽 |
| 状态栏 | 显示已就绪的本地字体数，以及阿里字体的实际来源 |

---

## 字体清单与授权

| 字体 | 来源 | 授权 | 是否开源 |
|---|---|---|---|
| 阿里巴巴普惠体 3.0（4 字重） | `fonts/`（随附） | 官方免费商用 | **否** |
| Noto Sans SC / Noto Serif SC（思源黑体 / 宋体） | `fonts/`（随附） | SIL OFL 1.1 | 是 |
| Inter / IBM Plex Sans / Geist / Public Sans / Space Grotesk / DM Sans / Manrope / JetBrains Mono | `font.onmicrosoft.cn`（运行时加载） | SIL OFL 1.1 | 是 |
| 系统字体（苹方 / 微软雅黑） | 操作系统 | 不可分发，仅作对照 | — |
| 本页面（HTML / CSS / JS） | 本项目 | 未经许可请勿转载 | **否** |

### 授权说明

- **阿里巴巴普惠体 3.0**：全球永久免费正版商用。3.0 版法律声明已**删除** 1.0/2.0 里「不得上传、发布、转载字体文件」的条款；现行禁止事项为：逆向 / 破解取源码、删改法律声明、单独定价出售 / 出租 / 出借 / 转让 / 转授权、发布暗示与阿里存在合作背书的不实信息。
  - 自行托管（自有服务器、内网）风险很低；公开 CDN 或随产品分发前，请核对官方现行声明。
  - 官方声明：https://www.alibabafonts.com
- **思源黑体 / 思源宋体**：SIL OFL 1.1，可随产品分发（保留授权文件即可）。

---

## 常见问题

**Q：直接双击 `index.html` 能打开吗？**
A：能。页面布局、对比网格、样张都正常显示。唯一的差别在字体：多数浏览器（Chrome / Edge / Firefox）把 `file://` 页面视为不透明来源（origin: null），会拦截 `@font-face` 加载本地字体——包括和页面同目录的（CVE-2019-11730 之后的行为），此时中文字体和阿里字体会回退到系统字体。8 个拉丁字体走 CDN，不受影响。

**Q：为什么字体显示不出来，或者跟系统字体一样？**
A：接上一条——是 `file://` 打开导致的。在项目目录起个服务，用 `http://127.0.0.1:<端口>/index.html` 打开就能看到真实字形：

```bash
python -m http.server 8731      # Python
npx -y serve -l 8731 .          # Node
```

如果换了浏览器、或者带了 `--allow-file-access-from-files` 启动，`file://` 下也能加载本地字体——但这属于非默认配置，不要依赖它。

**Q：想换一批字体源怎么办？**
A：URL 参数覆盖，不用改代码：

```
index.html?alibaba=https%3A%2F%2Fcdn.example.com%2Ffonts%2F
```

也支持站点内相对路径（`/fonts/`）和本地绝对路径（会转成 `file://`，仅当页面本身也是 `file://` 打开时才有意义；此时能不能加载取决于浏览器，见上一条）。

**Q：仓库 / 页面体积太大，能瘦吗？**
A：删掉 `fonts/NotoSansSC-VF.ttf` 和 `fonts/NotoSerifSC-VF.ttf`（合计 42MB），页面里这两个字体会自动回退到系统字体，其余不受影响。

**Q：`font.onmicrosoft.cn` 是什么？为什么页面要依赖它？**
A：它是一个 **npm 镜像站**（和 unpkg 同类），代理 `@fontsource/*` 系列包。Fontsource 把 Google Fonts 里的开源字体打包成 npm 包，所以从镜像取到的就是**官方字体文件**——不是本站自制、也没有二次修改，只是换了个国内能稳定访问的域名。

之所以走它：8 个拉丁字体不打进项目（省体积），页面首次打开时按固定版本去取（如 `@fontsource-variable/inter@5.2.5`），之后走浏览器缓存。取到的是 **latin 子集**（每个约 100–300 KB），不含中文字形；中文由本项目 `fonts/` 提供，两者不重叠。

镜像打不开时会自动回退到系统字体，页面不会报错、也不会卡住。想彻底离线或换源，把 `index.html` 顶部 `<style>` 里对应的 `@font-face` 的 `src` 改成本地文件或自己的 CDN 地址即可。

---

## 维护

**改字体来源**：改 URL 参数即可，见上。默认走同级 `fonts/`。

**更新字体文件**：替换 `fonts/` 下的同名文件即可，页面会自动用新的（注意浏览器缓存，强刷一下）。

**改页面**：`index.html` 是单文件，CSS 在 `<style>`、JS 在 `<script>`，改完刷新即可。阿里字体的 `@font-face` 由 `<head>` 里的脚本动态注入，不要用静态 `@font-face` 覆盖它。
