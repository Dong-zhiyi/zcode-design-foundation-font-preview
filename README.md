# 字体样张页 · design-foundation

一个自包含的静态页面，用来预览 design-foundation 的 13 个候选字体、挑字体用。
整个目录扔到任意静态服务器上就能用。

```
zcode-design-foundation-font-preview/
  index.html
  fonts/
    AlibabaPuHuiTi-3-45-Light.woff2
    AlibabaPuHuiTi-3-55-Regular.woff2
    AlibabaPuHuiTi-3-65-Medium.woff2
    AlibabaPuHuiTi-3-75-SemiBold.woff2
    NotoSansSC-VF.ttf
    NotoSerifSC-VF.ttf
```

## 部署

把 `index.html` 和 `fonts/` **放在同一个目录下**上传到服务器即可，两者必须同级——页面用相对路径 `./fonts/...` 加载字体。

- Nginx / OSS / COS / GitHub Pages / Vercel / Netlify：直接上传，无需配置
- 访问地址形如 `https://你的域名/zcode-design-foundation-font-preview/`（或 `.../zcode-design-foundation-font-preview/index.html`）

## ⚠️ 不要双击 index.html 打开

浏览器把 `file://` 页面视为不透明来源（origin: null），会拦截 `@font-face` 加载**任何**本地字体文件——包括和页面同目录的（CVE-2019-11730 之后的 Chrome / Edge / Firefox 都这样）。

所以：**必须通过 http(s) 访问**。本地想预览的话，在项目目录起个服务：

```bash
# Python
python -m http.server 8731
# Node
npx -y serve -l 8731 .
```

然后打开 `http://127.0.0.1:8731/index.html`。

## 换字体来源（可选）

默认用同级的 `fonts/`。想临时换源时用 URL 参数：

```
index.html?alibaba=https%3A%2F%2Fcdn.example.com%2Ffonts%2F
```

## 页面里的 13 个字体

| 字体 | 来源 | 授权 |
|---|---|---|
| Inter / IBM Plex Sans / Geist / Public Sans / Space Grotesk / DM Sans / Manrope / JetBrains Mono | `font.onmicrosoft.cn`（Fontsource 镜像，运行时加载） | SIL OFL 1.1 |
| Noto Sans SC / Noto Serif SC | `fonts/`（已随附） | SIL OFL 1.1 |
| 阿里巴巴普惠体 3.0（4 字重） | `fonts/`（已随附） | 官方免费商用（**非 OFL**） |
| 系统字体（苹方 / 微软雅黑） | 系统 | 不可分发，仅作对照 |

## 授权提醒

- **阿里巴巴普惠体 3.0**：全球永久免费正版商用。3.0 版法律声明已删除 1.0/2.0 里「不得上传、发布、转载字体文件」的条款；现行禁止事项为逆向/破解取源码、删改法律声明、单独定价出售/出租/出借/转让/转授权、发布暗示与阿里存在合作背书的不实信息。自行托管（自有服务器、内网）风险很低；公开 CDN 或随产品分发前请核对官方现行声明。官方声明：https://www.alibabafonts.com
- **思源黑体 / 思源宋体**：SIL OFL 1.1，可随产品分发（保留授权文件即可）。

## 想缩小体积？

删掉 `fonts/NotoSansSC-VF.ttf` 和 `fonts/NotoSerifSC-VF.ttf`（合计 42MB），
页面里这两个字体会自动回退到系统字体，其余不受影响。
