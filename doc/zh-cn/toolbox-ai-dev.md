# 用 AI 开发工具

工具箱的 **「创建工具」** 会生成一个完整的工具工程目录，再交给 AI 编辑器实现界面和逻辑。不需要手写代码，用自然语言描述需求即可。

---

## ✅ 前提条件

- 电脑上已安装以下任一 AI 工具：**Cursor**、**Codex**、**TRAE**、**TRAE CN**、**Qoder**
- 如果工具需要读写工程数据，请先在 Designer 中打开对应工程

---

## 🛠️ 创建工具

1. 打开 **工具箱**
2. 点击 **「创建工具」**
3. 填写工具信息
4. 点击 **「创建工具」**，进入工具设计页

| 字段 | 说明 |
| --- | --- |
| **工具名称** | 显示在卡片和窗口上的名称，必填 |
| **工具图标** | 可选，支持 PNG / JPEG / WebP / SVG，建议 256×256、不超过 300KB；留空由 AI 生成 |
| **工具 ID** | 可选，反向域名格式（如 `com.example.image-converter`）；留空自动生成 |
| **外观风格** | 默认的深浅色与视觉风格；如果需求中明确指定了风格，AI 会以需求为准 |
| **使用场景** | 可多选：工具箱、工作台、组件菜单，默认只选工具箱 |
| **作者** | 可选，显示在工具卡片上 |

### 使用场景怎么选

| 场景 | 适用情况 |
| --- | --- |
| **工具箱** | 独立小工具，如格式转换、字体裁剪、编码计算 |
| **工作台** | 需要读取或修改当前工程，如批量改样式、分析资源占用 |
| **组件菜单** | 希望从画布或组件树的右键菜单直接对某个组件使用 |

场景可以同时多选。创建后如需调整，可让 AI 修改工具目录中 `plugin.json` 的 `contexts` 字段。

---

## 🧩 可以开发哪些工具

工具运行在沙箱窗口中，只能通过宿主提供的能力与 Designer 交互，不能直接访问任意文件或系统进程。创建前先对照下表，确认需求是否在能力范围内；开发时由 AI 在 `plugin.json` 的 `permissions` 中声明对应权限。

### 按需求选型

| 想做的工具类型 | 典型例子 | 需要的能力 / 场景 |
| --- | --- | --- |
| **文件处理小工具** | 图片格式转换、批量重命名导出、打开结果文件夹 | `ui.openFile` / `ui.saveFile`、`image.convert`、`system.openExternal`；场景选 **工具箱** 即可 |
| **工程文件处理** | 合并多个 `.bkprj`、另存工程副本、对比工程差异 | `project.read`、`project.saveAs`；可在工具箱或工作台运行 |
| **工程分析 / 只读检查** | 资源占用统计、事件死链检查、页面结构浏览 | `project.documentRead`（或 `project.readCurrent` / `workbench.getProjectSnapshot`）；场景需含 **工作台** |
| **批量改工程** | 批量改样式/属性、批量加动画或事件、按规则清理组件 | `project.documentWrite`（`project.applyOperations`）；场景需含 **工作台** |
| **往画布插入组件** | 样式预设库、组件模板一键添加 | `workbench.addComponent` 或 `project.documentWrite`；场景需含 **工作台**（或组件菜单） |
| **真实 LVGL 预览** | 组件样式画廊缩略图、整页截图对比、自定义预览窗 | `preview.render` / `preview.renderPages`、`runtime.lvgl`、`assets.read` |

### 宿主能力一览

| 能力 | 权限名 | 可用场景 | 作用 |
| --- | --- | --- | --- |
| `ui.openFile` | `ui.openFile` | 工具箱 / 工作台 | 打开系统文件选择框，返回路径 |
| `ui.saveFile` | `ui.saveFile` | 工具箱 / 工作台 | 打开系统保存对话框，返回路径 |
| `ui.message` | `ui.message` | 工具箱 / 工作台 | 显示原生消息框 |
| `ui.openDoc` | `ui.openDoc` | 工具箱 / 工作台 | 在独立窗口打开本工具的使用文档 |
| `image.convert` | `image.convert` | 工具箱 / 工作台 | 图片格式转换与缩放（PNG / JPEG / BMP / GIF / TIFF） |
| `system.openExternal` | `system.openExternal` | 工具箱 / 工作台 | 打开 http / https / mailto 链接 |
| `project.read` | `project.read` | 工具箱 / 工作台 | 通过文件框选择并读取 `.bkprj` 工程 |
| `project.saveAs` | `project.saveAs` | 工具箱 / 工作台 | 将工程另存为新的 `.bkprj`（不会覆盖已有文件） |
| `project.readCurrent` | `project.readCurrent` | 仅工作台 | 读取当前工作台工程的已保存 `.bkprj`（只读） |
| `project.getSnapshot` | `project.documentRead` | 仅工作台 | 读取当前工程内存快照（摘要 / 当前页 / 全部） |
| `project.getScene` | `project.documentRead` | 仅工作台 | 读取指定页面的 LVGL 场景，可交给运行时渲染 |
| `project.applyOperations` | `project.documentWrite` | 仅工作台 | 批量修改组件、页面、动画、事件；支持事务与一次撤销 |
| `workbench.getProjectSnapshot` | `workbench.getProjectSnapshot` | 仅工作台 | 同 `project.getSnapshot`（兼容旧权限名） |
| `workbench.addComponent` | `workbench.addComponent` | 仅工作台 | 向当前工作台页面添加组件并应用属性 / 样式 |
| `preview.render` | `preview.render` | 工具箱 / 工作台 | 用真实 LVGL 批量渲染组件预览图（单次最多 20 项） |
| `preview.renderPages` | `preview.renderPages` | 仅工作台 | 用真实 LVGL 渲染工作台页面截图（单次最多 20 页，工程需已保存） |
| `runtime.lvgl` | `runtime.lvgl` | 工具箱 / 工作台 | 在工具窗口内嵌 LVGL 运行时（加载场景、截图、输入等） |
| `runtime.resolveResource` | `assets.read` | 仅工作台 | 为运行时解析当前工程的图片 / 字体资源 |

补充说明：

- 声明了 `project.documentRead` / `project.documentWrite`、`assets.read`、`project.readCurrent`、`preview.renderPages` 或任意 `workbench.*` 的工具，卡片上会显示 **工程联动** 标签。
- 仅工作台可用的能力，必须从工作台工具栏（或组件菜单）启动，并以 **「以工作台模式运行」** 调试。
- 工具不能直接读写任意磁盘路径：文件路径只能来自系统对话框，或由宿主在工程联动时提供。
- 界面交互、本地计算结果、持久化偏好（`storage`）不依赖上表能力，可在沙箱内自由实现。

向 AI 描述需求时，尽量写清「是否读写当前工程」「是否要真实 LVGL 预览」「输入输出是什么」，便于它选择正确的权限与场景。

---

## 🤖 让 AI 开始开发

1. 在设计页点击 **「AI开发」**
2. 在菜单中选择已安装的 AI 编辑器
3. 首次使用会自动安装 MCP 和工具开发 Skill，并在 AI 编辑器中打开当前工具目录

在 AI 编辑器中直接描述需求，例如：

```text
做一个图片格式转换工具：
- 支持拖入 PNG、JPG、WebP 批量转换
- 可以设置输出格式、质量和缩放比例
- 转换前显示每张图片的尺寸和体积
- 转换完成后可以一键导出到指定文件夹
- 界面延续当前目录 README 中的风格
```

或工程联动类需求：

```text
做一个资源占用分析工具（工作台场景）：
- 读取当前工程快照，统计页面、组件、图片和字体
- 估算 Flash / RAM 占用并给出建议
- 用表格展示结果，支持导出报告
```

AI 会直接创建和修改工具目录中的文件。设计页会监听目录变化，保存后自动刷新预览，可以边看效果边继续提修改意见。

---

## ▶️ 运行与调试

设计页顶部提供以下操作：

| 按钮 | 作用 |
| --- | --- |
| **运行** | 在独立窗口打开工具；下拉菜单可选择以工具箱或工作台模式运行 |
| **元信息** | 修改名称、ID、版本、作者、描述和图标 |
| **使用文档** | 打开工具的 `doc.md`，确认文档与功能一致 |
| **安装** | 把当前开发中的工具安装到 **「已安装」** 标签页 |
| **导出** | 生成 `.bkplugin` 安装包，用于分享或备份 |

以工作台模式运行时，工具会绑定当前打开的工程，可以直接验证读取和写入工程的能力。

---

## 📦 发布与分享

1. 确认 `doc.md` 已写明功能、操作流程和参数
2. 点击 **「导出」** 生成 `.bkplugin` 安装包
3. 其他人拿到安装包后，在工具箱中点击 **「导入安装包」** 即可安装

---

## ❓ 常见问题

**「AI开发」下拉里没有我的 AI 工具**
工具开发目前支持 Cursor、Codex、TRAE、TRAE CN 和 Qoder。请先安装并完成配置，再重新打开工具箱。

**AI 修改后预览没有变化**
设计页会自动监听工具目录并刷新。若未更新，重新打开工具或点击 **「运行」** 查看最新效果。

**工具读不到当前工程**
检查创建工具时是否勾选了 **工作台** 场景，并从 **「运行」→「以工作台模式运行」** 启动。

**想做的功能不在能力列表里**
对照上文 [可以开发哪些工具](#可以开发哪些工具)。若宿主尚未提供对应能力（例如任意网络请求后端、直接写系统文件），当前无法实现，可改用已有能力组合，或等待后续平台扩展。

**安装包保存在哪里**
点击 **「导出」** 后按提示选择保存位置，生成的 `.bkplugin` 文件即安装包。

---

**相关文档**：[工具箱与插件](toolbox.md) | [内置工具](toolbox-builtin.md)
