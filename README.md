# Lanhu UI Review Codex 插件

`lanhu-ui-review` 是一个 Codex 插件，用于辅助校对 App 或 Web 页面与蓝湖设计稿的一致性。它会引导 Codex 检查蓝湖设计中的尺寸、间距、颜色、字体、圆角、图标等信息，并对项目中的 UI 代码做展示层校准。

## 前置条件

使用前请先确认已准备好：

1. 已安装 Codex 桌面端，或正在使用支持 Codex 插件的环境。
2. 已安装 Chrome 浏览器。
3. 已安装并启用 Codex 的两个基础插件：
   - Chrome 插件：用于打开/检测蓝湖页面、读取浏览器状态。
   - Computer Use 插件：用于点击蓝湖设计图层、读取视觉检查面板中的尺寸和样式信息。
4. 已登录蓝湖账号，且有目标设计稿访问权限。
5. 本地项目可以正常运行、预览或构建。
6. 如果校对 Flutter 项目，建议提前确认：
   - `flutter pub get` 已完成。
   - 目标页面可以在模拟器、真机或 Web 环境打开。
   - 项目可以正常执行 `dart analyze` 或 `flutter analyze`。

## 安装

先安装 `lanhu-ui-review` 依赖的两个基础插件：

```sh
codex plugin add chrome@openai-bundled
codex plugin add computer-use@openai-bundled
```

先添加插件市场：

```sh
codex plugin marketplace add https://github.com/Todd-Liang/lanhu-ui-review-plugin
```

然后安装 `lanhu-ui-review` 插件：

```sh
codex plugin add lanhu-ui-review@study-team
```

安装完成后，建议新开或重启 Codex 线程，让 Chrome、Computer Use 和 `lanhu-ui-review` 的能力重新加载。

## 推荐准备工作

为了提高校对效率，建议开始前先做这些准备：

1. 打开需要校对的项目。
2. 启动 App 或 Web 页面，并进入目标页面。
3. 在 Chrome 中提前登录蓝湖。
4. 可以提前打开需要校对的蓝湖设计稿页面。

提前打开蓝湖页面不是必须的。你也可以直接让 Codex 使用插件，等待插件提示你打开或确认蓝湖页面。提前打开只是能减少等待和来回确认，让校对开始得更快。

## 使用方式

在 Codex 线程中直接说明要使用 `lanhu-ui-review` 即可，例如：

```text
使用 lanhu-ui-review 校对会员中心页面和蓝湖设计稿。
```

也可以写得更具体：

```text
使用 lanhu-ui-review 校准设置页，重点检查间距、字体、颜色和按钮尺寸。
```

英文提示也可以：

```text
Use lanhu-ui-review to calibrate the settings page.
Use lanhu-ui-review to correct the membership center page.
Use lanhu-ui-review to check this page against Lanhu.
```

## 适用场景

这个插件适合用于：

- Flutter 页面与蓝湖设计稿校对。
- Web 页面视觉还原检查。
- iOS 或 Android 页面 UI 校准。
- 检查字体、字号、颜色、间距、圆角、图标尺寸。
- 对已有页面做 UI-only 修正。

## 工作方式

插件会引导 Codex：

1. 确认要校对的目标页面和蓝湖设计稿。
2. 读取蓝湖中的关键视觉信息。
3. 对照本地页面实现，找出差异。
4. 修改展示层代码，尽量不改业务逻辑。
5. 汇总已校准的项目和仍需人工确认的点。

## 注意事项

- 插件主要用于 UI 校准，不建议同时修改业务逻辑。
- 如果页面涉及登录、权限、验证码或账号操作，Codex 可能会要求你手动确认。
- 如果蓝湖页面没有提前打开，插件会提示你打开或确认对应设计稿。
- 校对完成后，建议运行格式化、静态分析和相关测试。

## 插件内容

- `.agents/plugins/marketplace.json` 定义 `study-team` 插件市场入口。
- `plugins/lanhu-ui-review/.codex-plugin/plugin.json` 定义插件元信息。
- `plugins/lanhu-ui-review/skills/lanhu-ui-review/SKILL.md` 定义校对流程。
- `plugins/lanhu-ui-review/skills/lanhu-ui-review/agents/openai.yaml` 定义专用 agent。
- `plugins/lanhu-ui-review/skills/lanhu-ui-review/references/ui-calibration-checklist.md` 提供 UI 校准检查清单。
