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

值得覆盖的流程：打卡按钮切换（`[data-action="toggle-mod"]`，模块 id 见
`defaultModConfig()`，默认顺序 fitness/words/longs/reading）、笔记字段
（`[data-field="模块id:字段id"]`，如 `reading:summary`；多字段模块需先点
`open-panel`）、必选/选做进度分开统计（`.today-meta` 文案「必选 x/y · 选做 z/w」）、
「设置」页打卡项管理（`data-medit` 改名/图标/必选，`mod-up/down/del/add`，
`field-add/del`、`data-fedit` 字段改名，删除有 confirm 弹窗）、待办增删勾选、
reload 后 localStorage 持久化、旧版 v1 数据（english/fitness 结构）自动迁移、
「记录」页日历彩点与连续天数、点历史日期补卡、每日固定任务。

## 注意

- 日历格子和「去编辑」按钮共用 `data-date` 属性，选择器要用 `.cal-cell[data-date=…]`。
- GitHub 同步需要真实 Token，本地验证时跳过（未配置时应用显示「本地模式」即正常）。
- fullPage 截图中 sticky 页头 / fixed 底栏会出现在页面中部，是截图机制的正常现象。
