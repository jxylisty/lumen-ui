# Lumen UI

> 双主题设计系统：浅色清爽工作台 / 深色琉璃。零依赖、零构建，纯 CSS 变量驱动，两个文件开箱即用。
>
> A dual-theme design system for dashboards and admin panels. Zero dependencies, zero build step.

**在线预览**：clone 后直接用浏览器打开 `index.html`。

---

## 特点

- **零依赖、零构建** —— 两个 CSS 文件 + 一个 5KB 的 JS，直接丢进项目就能用
- **双主题** —— 浅色工作台与深色琉璃共用一套变量，切换只改 `<html data-theme>`
- **`color-mix()` 派生** —— 每个状态色（成功/警告/危险/紫/蓝）自动派生出背景、边框、光晕三档，不用手写几十个色值
- **强调色轮换** —— 12 个预置强调色，徽章、图表、标签按需取用
- **跟随系统** —— 未手动选择时读 `prefers-color-scheme`
- **尊重减弱动效** —— `prefers-reduced-motion` 下关闭全部动画
- **沉浸模式** —— 可选的全景壁纸 + 毛玻璃变体（`data-ui-style="immersive"`）

## 快速开始

```html
<!DOCTYPE html>
<html lang="zh-CN" data-theme="light">
<head>
  <script src="src/theme.js"></script>
  <link rel="stylesheet" href="src/lumen-tokens.css">
  <link rel="stylesheet" href="src/lumen.css">
</head>
<body>
  <button class="btn primary">按钮</button>
  <span class="badge a1">徽章</span>
  <i data-ic="grid"></i>
</body>
</html>
```

`theme.js` 必须放在 `<head>` 里同步加载，否则首屏会闪一下错误主题。

## 使用

### 切换主题

```js
lumenToggleTheme();          // 在明暗之间切换
lumenSetTheme("dark");       // 固定为深色
lumenTheme();                // 当前主题
```

选择会写进 `localStorage`，刷新后保持。也可直接用属性：

```html
<html data-theme="dark">
```

### 图标

用 `data-ic` 声明，`theme.js` 自动填充 Lucide 风格的线性 SVG：

```html
<i data-ic="grid"></i>
<i data-ic="settings"></i>
<i data-ic="check"></i>
```

可用图标见 `src/theme.js` 里的 `LumenIcons`（40 个内置）。

### 强调色

```html
<span class="badge a1">a1</span>   <!-- a1 ~ a12 -->
<span class="tag" style="--tch: var(--accent-3)">自定义</span>
```

## 设计令牌

所有颜色、圆角、阴影都定义在 `lumen-tokens.css` 的 `:root` 里。改配色只改这一处：

```css
:root {
  --primary: #4f6bf6;        /* 主色 */
  --ok: #10b981;             /* 成功 */
  --warn: #d97706;           /* 警告 */
  --danger: #ef4444;         /* 危险 */
  --radius: 16px;            /* 圆角 */
  --shadow-md: ...;          /* 阴影 */
}
```

深色主题在 `html[data-theme="dark"]` 里覆盖同名变量，组件样式完全不用改。

### 变量分组

| 分组 | 用途 |
|---|---|
| `--bg` `--bg-sub` `--card` `--card-solid` | 背景层次 |
| `--text` `--text-sub` `--muted` | 文字层次 |
| `--border` `--border-strong` `--border-soft` | 边框层次 |
| `--primary` `--ok` `--warn` `--danger` `--purple` | 语义色（各带 `-soft` 变体） |
| `--accent-1` ~ `--accent-12` | 强调色轮换 |
| `--radius` `--radius-sm` `--shadow-sm/md/lg` | 形状与阴影 |
| `--chart-*` | 图表专用（网格、轨道、标签、色板） |
| `--font` `--mono` | 字体栈 |

## 组件清单

| 类名 | 说明 |
|---|---|
| `.btn` `.btn.primary` `.btn.danger` `.btn.small` | 按钮（含 loading / disabled 态） |
| `.input` `.select` | 输入控件（focus 有光晕） |
| `.switch` + `.slider` | 开关 |
| `.tag` `.tag.ok/.warn/.danger/.purple/.blue` | 小标签 |
| `.badge` + `.a1`~`.a12` | 带呼吸点的胶囊徽章 |
| `.status-pill` + `.ok/.warn/.error` | 状态指示（在线点有呼吸动画） |
| `.overlay` + `.modal` | 模态框（毛玻璃遮罩） |
| `.toast` | 底部居中提示 |
| `.code-block` `.form-card` `.hint` `.risk-tip` | 内容容器 |

## 沉浸模式（可选）

```html
<html data-theme="dark" data-ui-style="immersive">
```

深色下切换为紫粉琉璃 + 半透明卡片，配合全屏壁纸使用。浅色主题不受影响。

## 浏览器要求

`color-mix()` 需要 Chrome 111+ / Safari 16.2+ / Firefox 113+。不支持时状态色会退化为透明背景，组件仍可使用。

## License

MIT
