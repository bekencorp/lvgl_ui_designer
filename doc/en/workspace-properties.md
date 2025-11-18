# ⚙️ Properties Panel

The properties panel is used to edit properties, styles, and data of the selected component.

### 4.1 Basic Properties

#### Layout Properties

**Position and Size**
- **X Coordinate**: X-axis position of component top-left corner (relative to parent component)
- **Y Coordinate**: Y-axis position of component top-left corner (relative to parent component)
- **Width**: Component width
- **Height**: Component height

#### Component-Specific Properties

Each component type has its specific properties, for example:

**Label Properties**
- **Text**: Text content to display
- **Long Mode**: Long text handling method (wrap/scroll/ellipsis)


**Image Properties**
- **Src**: Image source (select from resource manager)

**Slider Properties**
- **Min Value**: Minimum value
- **Max Value**: Maximum value

### 4.2 Style Editor

The style editor is a core feature of the properties panel, providing complete LVGL style support.

#### Style Parts

Some components have multiple style parts that can be styled separately, for example:

- **Main**: Main body part
- **Scrollbar**: Scrollbar
- **Indicator**: Indicator (like slider's slider part, progress bar's fill part)
- **Knob**: Knob (like slider's drag point)
- **Items**: List items
- **Cursor**: Cursor

#### Style States

LVGL components support multiple states, each state can have different styles, for example:

- **Default**: Default state of component
- **Checked**: When checkbox, switch, etc. is checked
- **Focused**: When component has focus
- **Pressed**: When button is pressed
- **Disabled**: When component is disabled

#### Style Library Functions

**Save Style**
1. Edit component's style
2. Click "Save" button in style panel
3. Enter style name
4. Add description (optional)
5. Click save

**Apply Style**
1. Select target component
2. Click "Apply" button in style panel
3. Select style to apply from style library
4. Click apply

**Manage Style Library**
- **Delete Style**: Delete in style library

---

**Workspace Docs**: [← Back to Workspace](workspace.md) | [Canvas](workspace-canvas.md) | [Components](workspace-components.md) | [Tree](workspace-tree.md) | [Properties](workspace-properties.md) | [Events](workspace-events.md) | [Toolbar](workspace-toolbar.md) | [Shortcuts](workspace-shortcuts.md)
