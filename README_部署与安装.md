# FitNote PWA 第三版（可部署网站包）

本项目把 FitNote 网页版包装为 PWA（渐进式 Web App），可部署后添加到 iPhone / Android 主屏幕。

## 包含内容
- `index.html`：FitNote 主应用，保留饮食、零食/大餐、运动、月历、身体档案、照片上传等网页功能。
- `manifest.webmanifest`：应用名称、图标、独立窗口显示设置。
- `sw.js`：Service Worker，用于缓存应用外壳并支持基础离线打开。
- `icons/`：根据用户指定的小豹子图生成的安装图标。
- `下载与安装.html`：手机端安装说明页。

## 重要：先部署 HTTPS
PWA 安装通常要求 HTTPS（localhost 开发例外）。直接从聊天附件下载 HTML 或从手机“文件”应用打开，不等于安装 PWA。

### 免费部署方法（GitHub Pages）
1. 在 GitHub 新建一个仓库，例如 `fitnote-app`。
2. 解压本 ZIP，把里面的所有文件和 `icons` 文件夹上传到仓库根目录（不要只上传 ZIP 本身）。
3. 进入仓库 `Settings` → `Pages`。
4. 在 Build and deployment 里选择 `Deploy from a branch`，分支选 `main`，目录选 `/(root)`，保存。
5. 等待 GitHub Pages 发布完成，打开它给出的 `https://...github.io/.../` 地址。
6. 在 iPhone 上用 Safari 打开；点击分享按钮 → “添加到主屏幕” → “添加”。
7. Android 使用 Chrome 打开，点菜单 → “安装应用”或“添加到主屏幕”。

## 也可以使用其他 HTTPS 静态托管服务
把解压后的文件夹整体上传到支持 HTTPS 的静态托管服务即可。不要删除 `manifest.webmanifest`、`sw.js` 或 `icons` 文件夹。

## 数据和隐私
- 记录保存在当前浏览器来源的本地存储中，不会自动上传服务器。
- 换浏览器、换部署域名、清除浏览器数据都可能导致看不到旧记录；请在应用“我的”页面定期导出 JSON 备份。
- 离线功能需要至少在线打开一次，完成 Service Worker 缓存。
- 这是网页 PWA，不是 App Store 的原生安装包，也不是 `.ipa` 文件。
- 仍不调用付费 GPT API。

## 更新网站
更新后重新上传替换 `index.html` 或其他文件。Service Worker 缓存版本目前是 `fitnote-pwa-v3`；若以后大改静态资源，建议同步更新 `sw.js` 中的缓存版本号。
