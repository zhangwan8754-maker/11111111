# 每日打卡 ✅

一个手机、电脑都能用的打卡记录小应用，数据多设备互通。

## 📱 怎么打开

部署完成后，直接访问：

**https://zhangwan8754-maker.github.io/11111111/**

- **手机**：用浏览器打开上面的网址 → 浏览器菜单 → 「添加到主屏幕」，以后就能像 App 一样从桌面打开。
- **电脑**：浏览器打开同一个网址，收藏即可。

> 首次推送代码后，GitHub Actions 会自动部署（仓库的 Actions 标签页里可以看到进度），大约 1 分钟后网址生效。

## ✨ 功能

- **英语板块**
  - 📖 阅读打卡：附带笔记表单——这篇讲了什么、作者立场是什么、标出的难句、喜欢的句子
  - 🔤 单词打卡（可加备注）
  - 🧩 长难句打卡（可加备注）
- **💪 健身记录**：打卡 + 记录训练内容
- **📌 待办任务**：临时任务随手加；「设置」里可添加每天自动出现的固定任务
- **📅 打卡日历**：每月一览，彩点表示各项完成情况，点历史日期可补卡
- **🔥 统计**：每项的连续天数、本月次数、累计次数
- 深色模式自动跟随系统

## ☁️ 电脑手机数据互通（重要）

数据默认保存在浏览器本地。要让多台设备互通，需要配置一次 GitHub Token（约 2 分钟）：

1. 打开 GitHub 网页并登录 → 点右上角头像 → **Settings**
2. 左侧栏拉到最底部 → **Developer settings**
3. **Personal access tokens → Fine-grained tokens → Generate new token**
4. Token name 随便填（比如 `daka`）；Expiration（有效期）建议选最长
5. Repository access 选 **Only select repositories**，勾选本仓库 `11111111`
6. Permissions → Repository permissions → **Contents** → 选 **Read and write**
7. 点 **Generate token**，复制 `github_pat_` 开头的一长串
8. 打开打卡应用 → 「设置」标签页 → 粘贴 Token → 点「保存并同步」
9. 在其他设备上打开应用，粘贴**同一个** Token，数据即自动互通 ✅

说明：

- 打卡数据保存在本仓库的 `data/checkin-data.json` 文件里，只有你自己能改。
- Token 只保存在你设备的浏览器中，同步请求直接发给 GitHub，不经过任何第三方服务器。
- 就算不配置同步，应用也能正常使用（数据仅存本机），还可以在「设置」里手动导出/导入 JSON 备份。

## 🛠 技术说明

- 纯静态单页应用（`index.html`），无需服务器、无任何依赖
- 通过 GitHub Pages 托管（`.github/workflows/pages.yml` 自动部署）
- 多设备同步 = 浏览器直接调用 GitHub API 读写 `data/checkin-data.json`，按日期做合并（取较新的一份），两台设备同时写入也不会互相覆盖
