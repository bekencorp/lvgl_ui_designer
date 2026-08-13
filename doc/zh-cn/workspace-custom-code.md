# 🔧 自定义代码

除了拖拽设计界面，您有时还需要补充自己的 C / MicroPython 逻辑。工具提供**两种方式**，请根据习惯选择，**不要在同一处重复写相同代码**。

---

## ⚖️ 一、两种方式有什么区别？

| 对比项 | **设计器内自定义代码** | **外部 IDE 修改生成文件** |
|--------|------------------------|---------------------------|
| **在哪里写** | 设计器属性面板、事件编辑器 | Keil、VS Code 等，打开 `beken_generated` 目录 |
| **保存在哪** | 工程文件（随项目一起保存） | 磁盘上的 `.c` / `.h` 文件 |
| **重新生成后** | 自动从工程写回 | 仅 `BEKEN_USER_CODE` 注释**里面**的代码会保留 |
| **适合谁** | 快速试逻辑、MicroPython 项目 | C 固件开发、对接 SDK、写复杂业务 |

**设计器内**包含三种入口，本质相同（都保存在工程里）：

- **页面自定义代码** — 页面加载时执行
- **事件 → 自定义代码** — 点击、值变化等交互时执行
- **事件 → 调用函数** — 在 `custom_func.c` 写实现，多处复用

**外部 IDE** 则直接改导出目录里的生成文件，但只能改注释标记内的区域：

```c
/* BEKEN_USER_CODE_BEGIN implementation */
// 您的代码写在这里
/* BEKEN_USER_CODE_END implementation */
```

> **提示**：设计器 **代码编辑器** 里，生成文件只能查看；可编辑的是 `custom_func.c` 和 `custom/` 目录。带 `BEKEN_USER_CODE` 的文件请用外部 IDE 打开。

---

## 🎨 二、设计器内怎么写？

### 1. 页面自定义代码

页面打开时需要额外初始化时使用。

1. 选中**页面（Screen）**
2. 属性面板 → **「自定义代码」** → **添加 / 编辑**
3. 填写 **#include 和变量**（写入 `page_*_init.c` 的 `BEKEN_USER_CODE includes` 内）、**功能实现**（写入 `init_page_xxx()` 的 `BEKEN_USER_CODE implementation` 内）

> **提示**：C 语言下，页面自定义代码与外部 IDE 追加代码共用同一对 `BEKEN_USER_CODE` 注释；设计器内容在重新生成时自动更新，其后手写内容会保留。

> **提示**：支持 **C 语言** 与 **MicroPython** 两个标签页。

### 2. 事件自定义代码

某个按钮点击、控件变化时需要执行逻辑时使用。

1. 选中组件 → 属性面板 **「事件」**
2. 添加事件，动作选 **「自定义代码」**
3. 填写 **#include 和变量** / **功能实现**
4. 点击 **确认** 保存

> **提示**：事件的 **#include 和变量** 写在 marker **外**的 `// custom event code` 处；**功能实现** 写在对应 `xxx_event_cb()` 回调内。

### 3. 调用函数

多个组件共用同一函数时使用。

1. 事件中动作选 **「调用函数」**，填写函数名（如 `handleButtonClick`）
2. 在 `custom_func.c` 中实现该函数

> **提示**：`custom_func.c` 和 `custom/` 目录重新生成时**不会覆盖**，可自由添加文件。

---

## 💻 三、外部 IDE 怎么写？

适用于 C 项目：用 Keil、VS Code 等打开 **`beken_generated`**（或项目设置里配置的导出目录）。

### 使用步骤

1. 找到文件中的 `BEKEN_USER_CODE_BEGIN` / `BEKEN_USER_CODE_END`
2. **只在两者之间**写代码，保存文件
3. 回到设计器，执行 **生成代码** 或 **生成+编译+运行**

### 注意事项

- 注释**外面**的内容是工具生成的，重新生成会被覆盖
- 改完 `beken_generated` 后，模拟器需执行 **生成+编译+运行** 才会用到最新代码（仅点「编译」不够）
- 在 `page_*_init.c` 的 marker 内追加代码时，请写在**页面属性自定义代码之后**，建议中间留一行空行

### 各文件可编辑区域

重新生成时，`BEKEN_USER_CODE` 注释**里面**的手写 C 代码会保留；**外面**由工具生成并覆盖。

| 文件 | 标记区域 | 适合写什么 |
|------|----------|------------|
| `page_*_init.c` | `includes`、`implementation`、**`file_tail`** | 页面级头文件/变量；`init_page_xxx()` 内追加逻辑；**文件末尾**追加代码 |
| `beken_ui.c` | `includes`、`implementation`、**`file_tail`** | `beken_ui_init()` 内扩展；**文件末尾**追加代码 |
| `beken_ui.h` | `includes` | 头文件引用、对外声明 |
| `event_runtime.c` | `includes`、`navigate_hook`、`switch_locale_hook`、**`file_tail`** | 跳转/切语言 hook；**文件末尾**追加代码 |
| `event_runtime.h` | `includes` | 头文件引用、对外声明 |
| `lv_i18n.c` | `includes`、`init_hook`、`set_locale_hook`、**`file_tail`** | 多语言扩展；**文件末尾**追加代码（启用多语言时生成） |
| `lv_i18n.h` | `includes` | 头文件引用、对外声明 |
| `basic_callback.c` | `includes`、**`file_tail`** | 头文件/变量；**文件末尾**追加代码 |

此外，以下路径**整文件**由用户维护，重新生成**不覆盖**：

- `custom_func.c` / `custom_func.h` — 「调用函数」事件实现
- `custom/` 目录 — 用户自建的 `.c` / `.h`

以下文件**请勿手动修改**（每次重新生成会完整覆盖）：

- `fonts/*.c`、`basic_callback.c`
- marker 外的组件初始化、事件框架、设计器内自定义代码对应区段

> **提示**：在文件中搜索 `BEKEN_USER_CODE` 可快速定位可保留的手写区域。

---

## 🔗 相关功能

- **[事件系统](workspace-events.md)** - 事件类型与动作配置
- **[工具栏](workspace-toolbar.md)** - 预览及代码生成
- **[快速开始](getting-started.md)** - 预览并生成代码

---

**工作台文档**：[← 返回工作台](workspace.md) | [事件系统](workspace-events.md) | [工具栏](workspace-toolbar.md)
