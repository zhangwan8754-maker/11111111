# 每日打卡 ✅

一个手机、电脑都能用的打卡记录小应用，数据多设备互通。

## 📱 怎么打开

**第一次需要手动开启 GitHub Pages（只需一次，约 30 秒）：**

1. 打开本仓库页面 → 点上方 **Settings**
2. 左侧栏找到 **Pages**
3. Build and deployment → Source 选 **Deploy from a branch**
4. Branch 选 **`gh-pages`**，目录保持 **`/ (root)`**，点 **Save**
5. 等大约 1 分钟，访问：

**https://zhangwan8754-maker.github.io/11111111/**

- **手机**：用浏览器打开上面的网址 → 浏览器菜单 → 「添加到主屏幕」，以后就能像 App 一样从桌面打开。
- **电脑**：浏览器打开同一个网址，收藏即可。

> 之后每次代码更新，GitHub Actions 会自动把网站发布到 `gh-pages` 分支，无需再做任何操作。

## ✨ 功能

- **打卡项（全部可自定义）**，默认顺序：
  - 💪 健身（非必选）：打卡 + 记录训练内容
  - 🔤 单词（必选，可加备注）
  - 🧩 长难句（必选，可加备注）
  - 📖 阅读（必选）：附带笔记表单——这篇讲了什么、作者立场是什么、标出的难句、喜欢的句子
- **🧩 打卡项管理**（设置页）：每一项都能改名、换图标、设为「每日必选 / 非必选」、调整顺序、删除，也能新增打卡项；每项要填的「记录问题」同样可以增删改。进度条和日历高亮只统计必选项
- **📌 待办任务**：临时任务随手加；「设置」里可添加每天自动出现的固定任务
- **📅 打卡日历**：每月一览，彩点表示各项完成情况，点历史日期可补卡
- **🔥 统计**：每项的连续天数、本月次数、累计次数
- 深色模式自动跟随系统

## ☁️ 电脑手机数据互通（重要）

数据默认保存在浏览器本地。要让多台设备互通，需要配置一次 GitHub Token（约 2 分钟）。

> ⚠️ **常见误区**：Token 在你的**个人账号设置**里创建，不是仓库的 Settings！如果你看到的是 Deploy keys，说明进了仓库的设置页，走错地方了。

**直达链接（登录后点开即到）：https://github.com/settings/personal-access-tokens/new**

1. 点上面的直达链接（手动路径：GitHub 任意页面 → 点**右上角自己的头像** → Settings → 左侧栏拉到**最底部** → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token）
2. Token name 随便填（比如 `daka`）；Expiration（有效期）建议选最长
3. Repository access 选 **Only select repositories**，在下拉里勾选本仓库 `11111111`
4. 往下找 Permissions → **Repository permissions** → 找到 **Contents** 一项 → 右侧选 **Read and write**
5. 拉到页面底部点 **Generate token**，复制 `github_pat_` 开头的一长串
6. 打开打卡应用 → 「设置」标签页 → 粘贴 Token → 点「保存并同步」
7. 在其他设备上打开应用，粘贴**同一个** Token，数据即自动互通 ✅

说明：

- 打卡数据保存在本仓库的 `data/checkin-data.json` 文件里，只有你自己能改。
- Token 只保存在你设备的浏览器中，同步请求直接发给 GitHub，不经过任何第三方服务器。
- 就算不配置同步，应用也能正常使用（数据仅存本机），还可以在「设置」里手动导出/导入 JSON 备份。

## 🛠 技术说明

- 纯静态单页应用（`index.html`），无需服务器、无任何依赖
- 通过 GitHub Pages 托管（`.github/workflows/pages.yml` 自动部署）
- 多设备同步 = 浏览器直接调用 GitHub API 读写 `data/checkin-data.json`，按日期做合并（取较新的一份），两台设备同时写入也不会互相覆盖
