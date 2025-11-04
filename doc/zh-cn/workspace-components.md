# 🧩 组件库

组件库提供了丰富的 LVGL UI 组件，分为系统组件和自定义组件两类。

### 2.1 系统组件库

#### 组件分类

**布局容器（Layout）**
- **Container** - 基础容器，用于组织其他组件
- **Window** - 窗口容器

**按钮（Button）**
- **Button** - 标准按钮
- **Image Button** - 图片按钮，支持多状态图片
- **Button Matrix** - 按钮矩阵，类似键盘布局

**表单输入（Form）**
- **Text Area** - 多行文本输入框
- **Checkbox** - 复选框
- **Switch** - 开关切换
- **Slider** - 滑动条
- **Dropdown** - 下拉选择框
- **Roller** - 滚轮选择器
- **Spinbox** - 数字调整框（带增减按钮）

**数据展示（Display）**
- **Label** - 文本标签
- **Span Group** - 富文本，支持多样式文本片段
- **Table** - 表格
- **List** - 列表

**图片媒体（Media）**
- **Image** - 图片显示

**可视化（Visualization）**
- **Arc** - 圆弧/进度环
- **Line** - 折线
- **QR Code** - 二维码
- **Barcode** - 条形码
- **LED** - LED 指示灯

**反馈提示（Feedback）**
- **Progress Bar** - 进度条
- **Spinner** - 加载动画
- **Message Box** - 消息提示框

**导航（Navigation）**
- **Tab View** - 标签页视图（开发中）
- **Tile View** - 平铺视图（开发中）

**高级组件（Advanced）**
- **Digital Clock** - 数字时钟
- **Calendar** - 日历
- **Keyboard** - 虚拟键盘
- **Scale** - 刻度尺/仪表盘

### 2.2 组件库功能

**搜索组件**
- 组件库顶部输入框：输入组件名称快速搜索

**组件预览**
- 鼠标悬停在组件上查看组件类型
- 每个组件都有对应的图标预览

**拖拽添加**
1. 在组件库中找到目标组件
2. 按住鼠标左键拖拽组件
3. 拖到画布中的目标位置
4. 松开鼠标完成添加

### 2.3 自定义组件库

#### 创建自定义组件

将常用的组件组合保存为模板，方便复用：

1. 在画布中设计好组件组合（例如：带图标的按钮）
2. 在组件树中选中组件
3. 右键选择 "创建自定义组件"
4. 输入组件名称和描述
5. 点击保存

#### 使用自定义组件

1. 切换到组件库的 "自定义组件" 选项卡
2. 找到保存的自定义组件
3. 拖拽到画布中使用
4. 自定义组件会保留所有属性和样式

#### 管理自定义组件
- **删除**：在自定义组件上选择 "删除"

---

**工作台文档**：[← 返回工作台](workspace.md) | [画布](workspace-canvas.md) | [组件库](workspace-components.md) | [组件树](workspace-tree.md) | [属性面板](workspace-properties.md) | [工具栏](workspace-toolbar.md) | [快捷键](workspace-shortcuts.md)
