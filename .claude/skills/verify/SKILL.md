---
name: verify
description: 本仓库（纯静态单页打卡应用）的运行与验证方法
---

# 运行与验证

纯静态站点，无构建步骤、无依赖。

## 启动

```bash
python3 -m http.server 8410 --bind 127.0.0.1   # 仓库根目录
# 打开 http://127.0.0.1:8410/index.html
```

## 驱动（Playwright）

```js
const { chromium } = require("playwright-core"); // npm i playwright-core
const browser = await chromium.launch({
  executablePath: "/opt/pw-browsers/chromium-1194/chrome-linux/chrome", // 远程环境预装
  headless: true,
});
```

值得覆盖的流程：4 个打卡按钮切换（`[data-action="toggle-mod"]`）、阅读笔记面板
（`open-panel` 后填 `[data-field="reading.*"]`）、待办增删勾选、reload 后
localStorage 持久化、「记录」页日历彩点与连续天数、点历史日期补卡、
「设置」页每日固定任务。

## 注意

- 日历格子和「去编辑」按钮共用 `data-date` 属性，选择器要用 `.cal-cell[data-date=…]`。
- GitHub 同步需要真实 Token，本地验证时跳过（未配置时应用显示「本地模式」即正常）。
- fullPage 截图中 sticky 页头 / fixed 底栏会出现在页面中部，是截图机制的正常现象。
