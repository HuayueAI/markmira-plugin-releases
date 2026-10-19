# Markmira 官方插件发布仓库

本仓库统一托管 Markmira 官方插件的编译产物。插件源码在独立的开发仓库维护，这里不包含 Markmira 主程序源码。

## 插件与版本

| 插件 ID | 用途 | Tag 示例 |
| --- | --- | --- |
| drawio | 本地 draw.io 流程图编辑器 | `drawio/v0.1.0` |
| excalidraw | 手绘白板 | `excalidraw/v0.1.0` |
| image | 图片查看 | `image/v0.1.0` |
| pdf | PDF 阅读与侧栏 | `pdf/v0.1.0` |
| text | 纯文本编辑 | `text/v0.1.0` |

所有插件独立使用语义化版本。发布某个插件不会更新其他插件；已发布版本不覆盖，修复时发布新版本。

请在 [Releases](https://github.com/HuayueAI/markmira-plugin-releases/releases) 按插件 ID 下载。不要使用 GitHub 的全仓库 `releases/latest` 查询某个插件版本，因为它可能返回另一个插件。

## 版本查询

每个插件的最新发布索引：

```text
https://raw.githubusercontent.com/HuayueAI/markmira-plugin-releases/main/plugins/<id>/latest.json
```

字段包括 `id`、`version`、`tag`、`hostApiVersion`、`downloadUrl`、`sha256`、`size`。历史索引位于 `plugins/<id>/versions/<version>.json`，更新客户端必须按 ID、版本和宿主 API 兼容性判断，下载后检查 SHA-256。

## 发布附件

- `<id>-<version>.zip`：可解压的插件根目录，包含 `manifest.json`、`plugin.js`、样式、图标、模板和所需本地资源。
- `manifest.json`：插件能力与宿主 API 版本。
- `release.json`：下载地址、体积和 SHA-256。
- `SHA256SUMS.txt`：插件压缩包校验值。

包内 `checksums.json` 记录文件清单及校验值，`build-info.json` 记录源码提交、工作区是否有未提交更改和构建时间。压缩包不包含私有仓库的 TypeScript/Vue 源文件、Git 数据或 source map；浏览器执行的 JavaScript 本身可被查看。

## 兼容性与信任

当前包格式是 `markmira-plugin-v1`，宿主 API 为 `1`。这些包先用于 Markmira 开发环境的本地扫描验证。安装版从网络下载、安装、回滚与自动更新的客户端机制尚未启用；发布索引已按独立更新设计。

校验值用于检测损坏或意外修改，不等同于数字签名。插件具有宿主授予的文件 API 能力，只安装可信发布者的插件。

draw.io 的编辑器与 PDF 的阅读资源随插件包分发，第三方许可证保留在对应资源目录中。外部图片、云服务等附加功能仍可能需要网络。
