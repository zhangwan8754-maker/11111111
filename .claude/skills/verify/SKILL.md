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

纸面日志（方向A）风格。值得覆盖的流程：打卡按钮切换（`[data-action="toggle-mod"]`，
模块 id 见 `defaultModConfig()`，默认顺序 fitness/words/longs/reading）、笔记字段
**始终内联可见**（`textarea.jinput`，`[data-field="模块id:字段id"]`，如 `reading:summary`，
无 open-panel）、引用体字段（`textarea.jinput.quote`，难句/好句默认，设置里
`field-style` 切换）、纸面页头（`.stamp` 连续天数印章、`.week-strip` 7天全天条、
`.ph-full` 庆祝语）、必选/选做进度（`.today-meta`）、textarea 自动增高（autoGrow）、
「设置」页打卡项管理（`data-medit`、`mod-up/down/del/add`、`field-add/del/style`、
`data-fedit`，删除有 confirm）、待办增删勾选、reload 持久化、旧版 v1 数据自动迁移、
未自定义配置(updatedAt=0)自动升级到新模板、「记录」页近7天(`.week-card-row`)+日历、
点历史日期补卡、每日固定任务。字体用系统衬线栈（无外部字体，兼顾离线/国内）。

## 注意

- 日历格子和「去编辑」按钮共用 `data-date` 属性，选择器要用 `.cal-cell[data-date=…]`。
- GitHub 同步需要真实 Token，本地验证时跳过（未配置时应用显示「本地模式」即正常）。
- fullPage 截图中 sticky 页头 / fixed 底栏会出现在页面中部，是截图机制的正常现象。
