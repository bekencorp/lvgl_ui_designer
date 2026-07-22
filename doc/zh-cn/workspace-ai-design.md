# AI 设计

AI 设计让你通过 **Cursor**、**Codex**、**TRAE** 或 **TRAE CN** 等 AI 工具，用自然语言描述界面需求。AI 会通过 MCP 工具直接修改 Beken LVGL UI Designer 画布上的内容，无需逐个手动拖拽组件。

---

## 📍 入口位置

1. 在 Designer 中**打开项目**并**进入工作台**
2. 点击工具栏 **「AI设计」** 按钮
3. 在下拉菜单中选择 **Cursor**、**Codex**、**TRAE** 或 **TRAE CN**（需已在电脑上安装对应 AI 工具）

下拉菜单会显示各 AI 工具的安装状态（已安装 / 未安装）。

---

## 🚀 首次使用与环境安装

首次从「AI设计」入口启动时，若 MCP 或 Skill 未安装或版本过旧，Designer 会自动检测并提示安装：

| 组件 | 作用 |
| --- | --- |
| **MCP** | 写入 AI 工具的全局配置，供 AI 调用 Designer 的页面、组件、属性等能力 |
| **Skill** | 复制到 AI 工具的全局 Skill 目录，指导 AI 如何理解项目并完成 UI 设计 |

安装完成后，AI 工具会打开当前项目目录下的 **`.ai-workspace`** 文件夹，并在其中开启对话。

### 确认 MCP 已加载

| 检查方式 | 正常表现 |
| --- | --- |
| Cursor / Codex：**设置 → MCP** | 列表中有 `beken_lvgl_ui_designer`，状态为已连接 |
| TRAE / TRAE CN：MCP 配置 | 已注册 `beken_lvgl_ui_designer` 且可正常连接 |

![Cursor MCP](/doc/images/mcp_status.png)

**若 MCP 未加载：** 完全关闭 Cursor / Codex / TRAE / TRAE CN，重新从 Designer 工具栏 **「AI设计」** 入口打开。**不要**手动打开其它文件夹或 `.ai-workspace` 以外的目录。

### 全局 AI 设置

在应用 **设置 → AI设置** 中可以：

- 查看 Bridge 运行状态
- 查看各 AI 工具的 MCP / Skill 安装状态与版本
- 手动安装、更新或卸载 AI 设计环境

> 安装或卸载 MCP / Skill 后，请**完全退出**对应 AI 工具，再从「AI设计」重新打开。

### 其它 AI 编辑器手动配置

如果使用的 AI 编辑器没有出现在 Designer 的 **「AI设计」** 下拉菜单中，但该编辑器支持 MCP 和 Skill，可以按本节手动配置。

Cursor / Codex / TRAE / TRAE CN 建议优先使用 **「AI设计」** 入口或 **设置 → AI设置** 自动安装；只有自动安装不可用或需要排查配置时，再参考本节手动配置。工具目录中已经包含 MCP 和 Skill，不需要额外下载。

请先找到 Beken LVGL UI Designer 的应用安装目录。MCP 和 Skill 都在该目录下的 `resources` 文件夹中。

MCP 脚本位于：

```text
<应用安装目录>\resources\mcp\lvgl-ui-designer-mcp.cjs
```

Skill 目录位于：

```text
<应用安装目录>\resources\ai-skill\beken-lvgl-ui-designer
```

#### 1. 配置 MCP

请在 AI 编辑器的 MCP 配置文件中加入 `beken_lvgl_ui_designer`。不同编辑器的 MCP 配置文件位置不同，请以对应编辑器文档为准。

常见配置路径示例：

Cursor：

```text
C:\Users\<用户名>\.cursor\mcp.json
```

TRAE：

```text
C:\Users\<用户名>\AppData\Roaming\Trae\User\mcp.json
```

TRAE CN：

```text
C:\Users\<用户名>\AppData\Roaming\Trae CN\User\mcp.json
```

Codex：

```text
C:\Users\<用户名>\.codex\config.toml
```

如果配置文件里已有其它 MCP server，Cursor / TRAE 只合并 `mcpServers.beken_lvgl_ui_designer` 这一项；Codex 只合并 `[mcp_servers.beken_lvgl_ui_designer]` 表，不要覆盖其它配置：

```json
{
  "mcpServers": {
    "beken_lvgl_ui_designer": {
      "type": "stdio",
      "command": "<应用安装目录>\\LVGL-UI-Designer.exe",
      "args": [
        "<应用安装目录>\\resources\\mcp\\lvgl-ui-designer-mcp.cjs"
      ],
      "env": {
        "ELECTRON_RUN_AS_NODE": "1",
        "LVGL_DESIGNER_BRIDGE": "http://127.0.0.1:39001"
      }
    }
  }
}
```

请将 `command` 改成当前电脑上应用安装目录下的 `LVGL-UI-Designer.exe` 路径，并将 `args` 中的路径改成同一目录下的 `resources\mcp\lvgl-ui-designer-mcp.cjs`。打包版使用应用自带的运行环境启动 MCP，不需要额外安装 Node.js。

#### 2. 安装 Skill

将应用目录中的 Skill 目录完整复制到 AI 编辑器的 Skill 目录。不同编辑器的 Skill 目录位置不同，请以对应编辑器文档为准。

常见目录示例：

Cursor：

```text
从：
<应用安装目录>\resources\ai-skill\beken-lvgl-ui-designer

复制到：
C:\Users\<用户名>\.cursor\skills\beken-lvgl-ui-designer
```

Codex：

```text
从：
<应用安装目录>\resources\ai-skill\beken-lvgl-ui-designer

复制到：
C:\Users\<用户名>\.codex\skills\beken-lvgl-ui-designer
```

TRAE：

```text
从：
<应用安装目录>\resources\ai-skill\beken-lvgl-ui-designer

复制到：
C:\Users\<用户名>\.trae\skills\beken-lvgl-ui-designer
```

TRAE CN：

```text
C:\Users\<用户名>\.trae-cn\skills\beken-lvgl-ui-designer
```

> Skill 目录必须完整复制，不能只复制 `SKILL.md`。

#### 3. 重启并验证

完成 MCP 配置和 Skill 复制后，请完全退出对应 AI 编辑器，再重新打开。随后启动 Designer，打开项目并进入工作台，在 AI 编辑器的 MCP 页面确认 `beken_lvgl_ui_designer` 已连接。

---

## 💬 如何使用 AI 进行设计

### 1. 启动 AI 工具

从工具栏「AI设计」选择已安装的 AI 工具。Designer 会确保 MCP / Skill 就绪，并打开该项目的 `.ai-workspace`。

### 2. 在聊天窗口描述需求

像跟设计助手对话一样，说明要完成的界面修改。示例：

```text
帮我把首页改成设备状态面板：顶部标题，中间显示温度和湿度，底部三个操作按钮。
```

**描述技巧：**

- 说明要改**哪个页面**、**整体布局**和各区域内容
- 可补充颜色、字号、间距等视觉要求
- **每次做一个明确改动**，看效果后再继续
- 需要图片或字体时，先通过[资源管理器](workspace-toolbar.md)导入，再让 AI 引用

### 3. 观察画布反馈

AI 通过 MCP 与 Designer 交互时，画布会有视觉反馈：

| 阶段 | 画布表现 |
| --- | --- |
| **读取 / 分析** | 扫描动效，提示「AI智能分析中...」 |
| **写入 / 修改** | 画布外围动效边框，表示正在修改界面 |

### 4. 确认或撤销修改

AI 完成一轮修改后，画布底部会出现 **「保存」** / **「撤销」**：

- **保存** — 接受本次 AI 修改，纳入项目撤销历史
- **撤销** — 恢复到 AI 开始本轮修改前的状态
- 若继续**手动编辑**或发起**新一轮 AI 对话**，未确认的修改会**自动保存**

---

## ✅ 支持的设计能力

AI 可通过 MCP 完成常见设计操作，例如：

- 查看项目摘要、页面列表与组件树
- 创建、删除、移动组件
- 修改组件属性与样式
- 创建或切换页面

部分高级能力（如复杂事件链、时间轴动画的精细调参等）可能暂不支持；AI 会说明限制，你可在此基础上手动完善。

---

## ❓ 常见问题

| 现象 | 处理方式 |
| --- | --- |
| **「AI设计」按钮灰色不可用** | 当前有 C 语言或 MicroPython 预览 / 编译 / 运行在进行。停止相关操作后再试。 |
| **下拉菜单显示「未安装」** | 电脑上未安装 Cursor、Codex 或 TRAE。请先安装对应 AI 工具。 |
| **提示无法修改界面 / 未打开项目** | 请先在 Designer 中打开项目并进入工作台，再从「AI设计」启动。 |
| **提示未进入工作台** | 请从项目管理页进入项目工作台，不要停留在首页。 |
| **提示工作区不匹配** | AI 对话窗口目录不是当前项目的 `.ai-workspace`。请关闭 AI 工具，从 Designer 工具栏「AI设计」**重新打开当前项目**，不要手动切换目录或打开其它项目。 |
| **AI 在终端执行 MCP 命令报错** | MCP 是 AI 工具内置能力，**不是**终端命令。说明 MCP 未正确加载，请从「AI设计」重新启动 AI 工具。 |
| **安装或更新 MCP 后仍异常** | 完全退出 Cursor / Codex / TRAE / TRAE CN 后重新从「AI设计」打开；或在 **设置 → AI设置** 中卸载 MCP 再重装。 |
| **AI 修改不符合预期** | 点击「撤销」，用更具体的描述重试（页面名、布局、组件类型、颜色等）。建议小步迭代。 |
| **Bridge 状态异常** | 在 **设置 → AI设置** 中点击「刷新状态」，确认 Bridge 正常运行后再使用。 |

---

## 💡 使用建议

1. **始终从 Designer 启动** — 确保 Designer 与 AI 工具打开的是同一项目
2. **保持工作台打开** — MCP 修改需要 Designer 处于工作台界面
3. **小步迭代** — 一次描述一个清晰目标，确认效果后再继续
4. **结合手动编辑** — 复杂交互、动画、多语言等可在 AI 搭好框架后，用[属性面板](workspace-properties.md)、[事件系统](workspace-events.md)等手动微调
5. **及时保存项目** — 确认 AI 修改后会纳入撤销历史；

---

## 🔗 相关功能

- **[工具栏](workspace-toolbar.md)** — AI 设计入口
- **[画布区域](workspace-canvas.md)** — 查看 AI 修改效果与确认条
- **[组件库](workspace-components.md)** — 了解可用组件类型

---

**工作台文档**：[← 返回工作台](workspace.md) | [画布](workspace-canvas.md) | [组件库](workspace-components.md) | [组件树](workspace-tree.md) | [属性面板](workspace-properties.md) | [事件系统](workspace-events.md) | [多语言](workspace-i18n.md) | [时间轴动画](workspace-animation.md) | [AI设计](workspace-ai-design.md) | [工具栏](workspace-toolbar.md) | [快捷键](workspace-shortcuts.md)
