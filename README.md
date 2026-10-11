# MOTED · 让光汇聚成你想要的形状

> 仓库 **cosmos** · 产品 **MOTED**

一个零依赖的单文件网页应用：输入文字或图片，粒子光效汇聚成形；鼠标划过、点击，星尘随之推开、爆炸、坠落。纯 Canvas 2D 实现，双击打开即用。

**在线体验：** http://cosmos.gaucn.com  
**开源仓库：** https://github.com/gaucn/cosmos  
**联系方式：** jiuchuan@gaucn.com

---

## 特性

- **单文件零依赖**：一个 `index.html` 搞定，HTML / CSS / JS 全部内联，无需构建、无第三方库。
- **文字 / 图片成型**：输入任意文字（或上传图片）自动采样轮廓，粒子平滑收敛成清晰字形或图形。
- **丰富交互**
  - 移动效果：推开 / 吸引 / 拖尾 / 光束 / 吞噬 / 无
  - 点击效果：爆炸 / 漩涡 / 海浪 / 坠落 / 无
  - 背景动画：轻飘 / 穿梭 / 静止
- **外观可定制**：原彩模式，6 套主题预设（纯白 / 湖蓝 / 落日 / 极光 / 樱粉 / 香槟），星尘色 / 背景色 / 漂浮色，支持 `#RRGGBB` 与 `#RRGGBBAA`（含透明度）。
- **粒子质感**：8 种材质（柔光 / 实心圆 / 同心圆 / 星芒 / 方块 / 雪花 / 光环 / 气泡）+ 8 种背景纹理（无 / 网格 / 点阵 / 噪点 / 扫描线 / 波纹 / 星云 / 暗角），密度、分散、大小均可调。
- **自动播放**：可设定触发位置（中心 / 随机）与间隔时长，循环演示。
- **导出与分享**：一键导出 PNG 图片、视频；分享链接一键复制。
- **移动端适配**：响应式布局，触屏可用。

## 快速开始

### 本地运行

下载 `index.html`，双击用浏览器打开即可（推荐 Chrome / Edge）。

也可以起一个本地静态服务：

```bash
# 任选其一
python -m http.server 8000
npx serve .
```

然后访问 `http://localhost:8000/index.html`。

### 部署

项目为纯静态页面，可直接托管到 GitHub Pages / Vercel / Netlify 或任意静态服务器。仓库根目录的 `index.html` 即入口文件，克隆/下载后开箱即用；自定义域名通过根目录的 `CNAME` 配置。

## 使用说明

- 顶部输入框：输入文字即成型；下方快捷词一键填入；「图片」按钮可上传图片采样成型。
- 设置面板分为四页：
  - **显示**：原彩、主题、星尘色、背景色、漂浮色
  - **粒子**：材质、纹理、密度、分散、大小
  - **效果**：移动效果、点击效果、背景动画、自动播放及触发设置
  - **分享**：复制分享链接、导出图片 / 视频
- 交互：鼠标划过触发「移动效果」，点击触发「点击效果」。

## 配置

页面初始化时会读取全局对象 `window.__MOTE__` 并覆盖默认值。把它写在主脚本之前（例如 `<head>` 内）即可：

```html
<script>
window.__MOTE__ = {
  text: '你好，世界！',
  hover: 'attract',
  click: 'explode',
  idle: 'drift',
  matter: 'glow',
  texture: 'none',
  autoSec: 10
};
</script>
```

可用字段：

| 字段 | 类型 / 取值 | 默认 | 说明 |
| --- | --- | --- | --- |
| `sourceType` | `text` \| `image` | `text` | 成型来源 |
| `text` | string | `〇` | 文字内容 |
| `imageData` / `imageName` | string | `null` | 图片 Base64 与文件名（`sourceType=image` 时） |
| `colorful` | bool | `false` | 原彩模式（彩色星尘） |
| `theme` | 主题 key | `white` | 主题预设 |
| `particleColor` | hex | `#FFFFFF` | 星尘色 |
| `bgColor` | hex | `#000000` | 背景色 |
| `floatColor` | hex \| 空 | 空 | 漂浮色；留空则跟随（原彩下为彩虹，否则跟随星尘色） |
| `matter` | 材质 key | `glow` | 粒子材质 |
| `texture` | 纹理 key | `none` | 背景纹理 |
| `density` | -3 ~ 4 | `0` | 密度 |
| `spread` | 0 ~ 200 | `100` | 分散（%） |
| `size` | 50 ~ 180 | `100` | 大小（%） |
| `hover` | `push` / `attract` / `trail` / `beam` / `devour` / `none` | `push` | 移动效果 |
| `click` | `explode` / `vortex` / `wave` / `fall` / `none` | `explode` | 点击效果 |
| `idle` | `drift` / `warp` / `still` | `still` | 背景动画 |
| `loop` | bool | `true` | 自动播放 |
| `autoPos` | `center` / `random` | `center` | 触发位置 |
| `autoSec` | number | `10` | 自动播放间隔（秒） |

## 导出

- **图片**：将当前画面导出为 `PNG`。
- **视频**：录制当前动画导出为视频，优先 `MP4`（H.264），浏览器不支持时回退 `WebM`。

## 项目结构

```
index.html     # 全部内容：结构 + 样式 + 脚本，零外部依赖
README.md      # 项目说明
LICENSE        # Apache License 2.0
NOTICE         # 版权与归属声明
CNAME          # GitHub Pages 自定义域名（cosmos.gaucn.com）
```

## 技术实现

- **渲染**：Canvas 2D，`globalCompositeOperation = 'lighter'` 加法混合实现发光叠色，逐帧半透明填充形成拖尾。
- **成型**：对文字 / 图片做像素采样得到目标点，粒子以缓动收敛到目标。
- **状态**：`cfg` 配置对象 + `state` 字符串状态机（forming / formed / fall / scatter）。
- **导出**：`canvas.toDataURL` 出图、`MediaRecorder` 录制视频。

无任何第三方库，无构建步骤。

## 浏览器支持

现代浏览器（Chrome / Edge / Safari / Firefox）均可运行。视频导出依赖 `MediaRecorder`，较旧的浏览器可能仅支持 `WebM`。

## 二次开发与宣传

欢迎基于本项目做二次开发、二次创作，或直接用于自己的产品、页面与教程。**如果你用到了它，建议在显眼位置标注本项目的开源地址**——这对我们是最大的支持，也是持续维护的动力。

- 开源仓库：https://github.com/gaucn/cosmos
- 在线体验：http://cosmos.gaucn.com

可以直接粘贴下面的片段：

**Markdown**

```markdown
粒子文字特效 [MOTED](https://github.com/gaucn/cosmos) · [在线体验](http://cosmos.gaucn.com)
```

**HTML**

```html
<em>基于 <a href="https://github.com/gaucn/cosmos" target="_blank" rel="noopener">MOTED 粒子文字特效</a> 构建</em>
```

**徽章（Badge）**

```markdown
[![Powered by MOTED](https://img.shields.io/badge/Powered%20by-MOTED-000000?style=flat-square)](https://github.com/gaucn/cosmos)
```

## 开源协议

本项目基于 [Apache License 2.0](LICENSE) 开源。你可以自由使用、修改、分发（包括商业闭源用途），需要遵守：

- 保留本项目的版权、许可声明与 [NOTICE](NOTICE) 文件；
- 若修改了源文件，需在文件中注明已做修改。

```
Copyright 2026 上海旧川科技有限公司

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

## 贡献

欢迎提交 Issue / PR：新增主题、材质、纹理，或改进性能与兼容性。提交前请保持「单文件、零依赖」的定位。

## 联系方式

- 邮箱：jiuchuan@gaucn.com
- 仓库：https://github.com/gaucn/cosmos

## 版权

© 2026 上海旧川科技有限公司
