# Build Tools with AI

**「Create Tool」** in the Toolbox generates a complete tool project folder. Hand it to an AI editor and describe what you want in natural language; no manual coding is required.

---

## ✅ Prerequisites

- Install one of these AI tools: **Cursor**, **Codex**, **TRAE**, **TRAE CN**, or **Qoder**
- If the tool needs project data, open the project in Designer first

---

## 🛠️ Create a Tool

1. Open the **Toolbox**
2. Click **「Create Tool」**
3. Fill in the tool details
4. Click **「Create Tool」** to open the tool design page

| Field | Description |
| --- | --- |
| **Name** | Shown on the card and tool window; required |
| **Icon** | Optional; PNG / JPEG / WebP / SVG, 256×256 recommended, up to 300KB. Leave empty to let AI generate one |
| **Tool ID** | Optional reverse-domain ID (e.g. `com.example.image-converter`); generated automatically when empty |
| **Appearance** | Default light/dark mode and visual style; an explicit style in your requirements takes priority |
| **Scenes** | Multi-select: Toolbox, Workspace, Component Menu; Toolbox is selected by default |
| **Author** | Optional; shown on the tool card |

### Choosing Scenes

| Scene | When to use |
| --- | --- |
| **Toolbox** | Standalone utilities such as format conversion, font subsetting, or encoding calculators |
| **Workspace** | Tools that read or modify the current project, such as batch style edits or resource analysis |
| **Component Menu** | Tools you want to launch for a component from the canvas or component tree context menu |

You can select several scenes. To change them later, ask the AI to edit the `contexts` field in `plugin.json`.

---

## 🧩 What Tools Can You Build

Tools run in a sandboxed window and can only talk to Designer through host capabilities. They cannot access arbitrary files or system processes. Before creating a tool, check the tables below to confirm your idea is in scope. During development, the AI declares the matching entries in `plugin.json` under `permissions`.

### Pick by Use Case

| Tool type | Examples | Capabilities / scenes |
| --- | --- | --- |
| **File utilities** | Image format conversion, batch export, open result folders | `ui.openFile` / `ui.saveFile`, `image.convert`, `system.openExternal`; **Toolbox** scene is enough |
| **Project-file tools** | Merge `.bkprj` files, save a project copy, compare projects | `project.read`, `project.saveAs`; Toolbox or Workspace |
| **Read-only project analysis** | Resource budget, dead-link checks, page structure browsers | `project.documentRead` (or `project.readCurrent` / `workbench.getProjectSnapshot`); scene must include **Workspace** |
| **Batch project edits** | Batch style/property changes, add animations or events, clean up components by rule | `project.documentWrite` (`project.applyOperations`); scene must include **Workspace** |
| **Insert components on canvas** | Style galleries, one-click component templates | `workbench.addComponent` or `project.documentWrite`; scene must include **Workspace** (or Component Menu) |
| **True LVGL previews** | Style-gallery thumbnails, full-page screenshots, custom preview panes | `preview.render` / `preview.renderPages`, `runtime.lvgl`, `assets.read` |

### Host Capability Catalog

| Capability | Permission | Scenes | What it does |
| --- | --- | --- | --- |
| `ui.openFile` | `ui.openFile` | Toolbox / Workspace | Open a system file picker and return paths |
| `ui.saveFile` | `ui.saveFile` | Toolbox / Workspace | Open a system save dialog and return a path |
| `ui.message` | `ui.message` | Toolbox / Workspace | Show a native message box |
| `ui.openDoc` | `ui.openDoc` | Toolbox / Workspace | Open this tool's documentation in a separate window |
| `image.convert` | `image.convert` | Toolbox / Workspace | Convert and scale images (PNG / JPEG / BMP / GIF / TIFF) |
| `system.openExternal` | `system.openExternal` | Toolbox / Workspace | Open http / https / mailto links |
| `project.read` | `project.read` | Toolbox / Workspace | Pick and read a `.bkprj` project via a file dialog |
| `project.saveAs` | `project.saveAs` | Toolbox / Workspace | Save the project as a new `.bkprj` (never overwrites an existing file) |
| `project.readCurrent` | `project.readCurrent` | Workspace only | Read the saved `.bkprj` of the current workspace project (read-only) |
| `project.getSnapshot` | `project.documentRead` | Workspace only | Read the in-memory project snapshot (summary / current page / all) |
| `project.getScene` | `project.documentRead` | Workspace only | Read a page's LVGL scene for runtime rendering |
| `project.applyOperations` | `project.documentWrite` | Workspace only | Batch-edit components, pages, animations, and events; supports a transaction and one undo |
| `workbench.getProjectSnapshot` | `workbench.getProjectSnapshot` | Workspace only | Same as `project.getSnapshot` (legacy permission name) |
| `workbench.addComponent` | `workbench.addComponent` | Workspace only | Add a component to the current workspace page with properties / styles |
| `preview.render` | `preview.render` | Toolbox / Workspace | Batch-render component previews with the real LVGL runtime (up to 20 items) |
| `preview.renderPages` | `preview.renderPages` | Workspace only | Render workspace page screenshots with the real LVGL runtime (up to 20 pages; project must be saved) |
| `runtime.lvgl` | `runtime.lvgl` | Toolbox / Workspace | Embed the LVGL runtime surface in the tool window (load scenes, screenshots, input, etc.) |
| `runtime.resolveResource` | `assets.read` | Workspace only | Resolve image / font assets from the current project for the runtime |

Notes:

- Tools that declare `project.documentRead` / `project.documentWrite`, `assets.read`, `project.readCurrent`, `preview.renderPages`, or any `workbench.*` permission show the **Project Linkage** badge.
- Workspace-only capabilities must be launched from the workspace toolbar (or component menu) and debugged with **「Run in Workspace Mode」**.
- Tools cannot read or write arbitrary disk paths: paths come only from system dialogs, or from the host during project linkage.
- UI interaction, local computation, and preference storage (`storage`) do not need the capabilities above and can be implemented freely in the sandbox.

When describing requirements to the AI, state clearly whether the tool reads/writes the current project, needs true LVGL previews, and what the inputs/outputs are, so it can pick the right permissions and scenes.

---

## 🤖 Let AI Build It

1. Click **「AI Development」** on the design page
2. Choose an installed AI editor
3. On first use, MCP and the tool-development Skill are installed automatically, and the AI editor opens the tool folder

Describe your requirements directly in the AI editor, for example:

```text
Build an image format converter:
- Accept PNG, JPG, and WebP files by drag and drop for batch conversion
- Let me set the output format, quality, and scale
- Show each image's dimensions and file size before conversion
- Export all results to a chosen folder in one click
- Follow the visual style described in the README in this folder
```

Or a project-linked example:

```text
Build a resource-budget analyzer (Workspace scene):
- Read the current project snapshot and count pages, components, images, and fonts
- Estimate Flash / RAM usage and give recommendations
- Show results in a table and support exporting a report
```

The AI creates and edits files in the tool folder. The design page watches the folder and refreshes the preview after each save, so you can review the result and keep refining.

---

## ▶️ Run and Debug

The design page toolbar provides:

| Button | Purpose |
| --- | --- |
| **Run** | Open the tool in its own window; the dropdown lets you run it in Toolbox or Workspace mode |
| **Metadata** | Edit the name, ID, version, author, description, and icon |
| **Documentation** | Open the tool's `doc.md` and confirm it matches the feature set |
| **Install** | Install the in-development tool into the **Installed** tab |
| **Export** | Generate a `.bkplugin` package for sharing or backup |

In Workspace mode, the tool binds to the currently open project so you can verify project read/write behavior directly.

---

## 📦 Publish and Share

1. Make sure `doc.md` covers the features, workflow, and parameters
2. Click **「Export」** to generate a `.bkplugin` package
3. Others can install it with **「Import Package」** in the Toolbox

---

## ❓ FAQ

**My AI tool is missing from the 「AI Development」 dropdown**
Tool development supports Cursor, Codex, TRAE, TRAE CN, and Qoder. Install and configure one of them, then reopen the Toolbox.

**The preview did not change after AI edits**
The design page watches the tool folder and refreshes automatically. If it still looks stale, reopen the tool or click **「Run」** to view the latest result.

**The tool cannot read the current project**
Check that **Workspace** was selected when creating the tool, and launch it with **「Run」→「Run in Workspace Mode」**.

**The feature I want is not in the capability list**
See [What Tools Can You Build](#what-tools-can-you-build). If the host does not expose a matching capability yet (for example a network backend or direct arbitrary filesystem write), it cannot be built today—combine existing capabilities, or wait for a future platform update.

**Where is the package saved**
After clicking **「Export」**, choose a location when prompted. The generated `.bkplugin` file is the package.

---

**Related:** [Toolbox and Plugins](toolbox.md) | [Built-in Tools](toolbox-builtin.md)
