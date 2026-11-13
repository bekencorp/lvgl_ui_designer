# Toolbox and Plugins

The Toolbox manages and runs tools. Each tool is a self-contained mini app (plugin) that runs in its own window. Closing a tool window does not affect Designer.

---

## 📍 Open the Toolbox

Click **「Toolbox」** in the top navigation bar.

The Toolbox has two tabs:

| Tab | Content |
| --- | --- |
| **Installed** | Built-in tools and tools installed from packages |
| **In Development** | Tools you created; continue designing, running, and installing them |

Buttons in the top-right corner:

| Button | Purpose |
| --- | --- |
| **Refresh** | Reload the tool list |
| **Import Package** | Install a `.bkplugin` tool package |
| **Create Tool** | Create a tool and open its design page to build it with AI |

---

## ▶️ Run a Tool

Click a tool card to open it in a separate window.

Card badges:

| Badge | Meaning |
| --- | --- |
| **Official** | Bundled with the application; no installation needed |
| **Project Linkage** | Can read or write pages, components, animations, and other data in the current project |
| **Component Menu** | Can be opened from the canvas or component tree context menu |

### Run from the Workspace

1. Open a project and enter the workspace
2. Click the **「Toolbox」** dropdown on the toolbar
3. Choose a tool; it binds to the current project and reads project data

### Run from the Component Menu

1. Right-click a component on the canvas or in the component tree
2. Choose a tool that supports the component menu
3. The tool opens with the selected component already loaded

> Tools run in a sandboxed window and can only use host capabilities declared in `plugin.json`. Undeclared capabilities are unavailable. For the full capability list and tool types you can build, see [Build Tools with AI](toolbox-ai-dev.md#what-tools-can-you-build).

---

## 📖 Read a Tool's Documentation

Click **「Documentation」** in the top-right corner of the tool window, or press **F1**.

Each tool documents its interface, workflow, parameters, and troubleshooting.

---

## 📦 Install, Uninstall, and Delete

**Install:** click **「Import Package」** → select a `.bkplugin` file. The tool appears under **Installed**.

**Uninstall:** right-click an installed tool card → **「Uninstall」**. Built-in tools cannot be uninstalled.

**In-development tools:** click a card to open its design page; right-click → **「Delete」** to permanently remove the tool folder and files.

---

**Related:** [Built-in Tools](toolbox-builtin.md) | [Build Tools with AI](toolbox-ai-dev.md)
