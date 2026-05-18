# 更新日志

本文件同时用于：

- 根目录版本更新记录维护
- GitHub Release 发布说明来源

书写规则：

- 每次发布新版本时，在顶部新增一个版本段
- 标题格式必须为 `## x.y.z - YYYY-MM-DD`
- 版本号必须与 Git tag 一致，例如 `1.0.0`
- GitHub Actions 会自动提取对应版本段内容作为 Release Notes

## 1.0.1 - 2026-05-18

### 新增

- 新增 GitHub Release workflow 模板
- 新增 `CHANGELOG.md` 版本发布说明约定
- 新增 `scripts/extract-release-notes.js` 用于自动提取发布说明

### 优化

- 版本化构建脚本调整为固定输出目录，并在产物中写入 `VERSION` 文件
- ZIP 文件名保留版本号，但解压后的根目录固定，便于本地反复加载扩展
- 版本号未变化时不再重写 `package.json` 与 `manifest.json`
- 完善 `README.md`、`docs/SETUP.md`、`docs/BUILD_VERSION.md` 的模板使用与发布说明

## 1.0.0 - 2026-05-18

### 新增

- 提供 `Vue 3 + Vite + Pinia` 的 Chrome 扩展基础模板
- 内置版本化构建脚本，支持普通构建、开发构建与 ZIP 打包
- 提供基础文档、GitHub Release workflow 模板与版本说明提取脚本

### 优化

- 普通版本化构建目录固定为 `output/chrome-plugin-vue3`
- ZIP 文件名保留版本号，但解压后的根目录固定为 `chrome-plugin-vue3`
- 构建产物新增无后缀 `VERSION` 文件，用于标记当前版本
