# chrome-plugin-vue3

一个基于 `Vue 3 + Vite + Pinia` 的 Chrome 扩展模板，适合快速起一个带基础工程化能力的浏览器插件项目。

模板内置：

- `Manifest V3` 基础结构
- `Vue 3` 页面入口与常用状态管理
- 版本化构建脚本
- ZIP 打包能力
- GitHub Release 自动发布工作流模板

## 开发命令

```bash
npm install
npm run dev
npm run build
npm run lint
npm run bv:dev
npm run bv -- 1.0.0
npm run bv:zip -- 1.0.0
```

`npm run bv:dev` 会在开发包的 `manifest.json` 中自动追加开发标识：

- 扩展名称追加 ` [DEV]`
- `version_name` 显示为 `<当前版本>-dev`

这样浏览器里可以和正式版直接区分。

## 构建产物规则

- 普通版本化构建输出目录固定为 `output/chrome-plugin-vue3`
- ZIP 文件名保留版本号，例如 `output/chrome-plugin-vue3_v1.0.0.zip`
- ZIP 解压后的根目录固定为 `chrome-plugin-vue3`
- 构建产物目录内会写入无后缀版本标记文件 `VERSION`

这个规则的目的是让本地反复加载已解压扩展时尽量保持目录稳定，避免因为目录名变化引起额外的插件实例切换问题。

## 项目结构

```text
src/
├─ components/     # 通用组件
├─ composables/    # 组合式逻辑封装
├─ content/        # 内容脚本入口
├─ stores/         # Pinia 状态管理
├─ utils/          # 工具函数
├─ background.js   # Service Worker 入口
├─ App.vue         # 页面主组件
└─ popup.js        # 页面入口
scripts/
├─ build-with-version.js      # 版本化构建脚本
└─ extract-release-notes.js   # 发布说明提取脚本
docs/
├─ SETUP.md
└─ BUILD_VERSION.md
.github/workflows/
└─ release.yml
```

## 本地加载扩展

1. 执行 `npm run bv -- 1.0.0`
2. 打开 `chrome://extensions/`
3. 开启「开发者模式」
4. 点击「加载已解压的扩展程序」
5. 选择 `output/chrome-plugin-vue3`
6. 如需确认当前构建版本，可查看 `output/chrome-plugin-vue3/VERSION`

## 发布流程

1. 更新 [CHANGELOG.md](./CHANGELOG.md)
2. 本地验证 `npm run bv -- 1.0.0`
3. 正式打包执行 `npm run bv:zip -- 1.0.0`
4. 提交代码并推送
5. 推送语义化 tag，例如：

```bash
git tag 1.0.0
git push origin 1.0.0
```

6. GitHub Actions 会自动：
   - 校验 `CHANGELOG.md` 中是否存在对应版本段
   - 执行 `bv:zip`
   - 创建 GitHub Release
   - 上传 ZIP 构建产物

## 模板初始化建议

基于这个模板创建新项目后，优先修改这些内容：

- `package.json` 中的 `name` / `description`
- `manifest.json` 中的扩展名称、描述、权限
- `icons/` 中的图标资源
- `README.md` 与 `CHANGELOG.md`
- `scripts/build-with-version.js` 里的 `PROJECT_NAME`，否则输出目录和 ZIP 文件名仍会保留模板名
- `.github/workflows/release.yml` 中的发布流程细节（如果你的仓库需要自定义）

## 相关文档

- [快速开始](./docs/SETUP.md)
- [版本化构建说明](./docs/BUILD_VERSION.md)
- [Chrome 扩展开发文档](https://developer.chrome.com/docs/extensions/)
