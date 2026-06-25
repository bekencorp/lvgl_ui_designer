# AI Design

AI Design lets you describe UI requirements in natural language using **Cursor** or **TRAE**. The AI modifies the canvas in Beken LVGL UI Designer through MCP tools, without placing every component manually.

---

## 📍 Entry Point

1. **Open a project** and **enter the workspace** in Designer
2. Click the **「AI Design」** button on the toolbar
3. Choose **Cursor** or **TRAE** from the dropdown (the corresponding AI tool must be installed on your computer)

The dropdown shows whether each AI tool is installed.

---

## 🚀 First-Time Setup

When you launch from **AI Design** for the first time, Designer checks whether MCP and Skill are installed and up to date:

| Component | Purpose |
| --- | --- |
| **MCP** | Writes global configuration into the AI tool so it can call Designer APIs for pages, components, properties, and more |
| **Skill** | Copies guidance into the AI tool's global Skill directory so the AI knows how to design UI in your project |

After setup, the AI tool opens the **`.ai-workspace`** folder under the current project directory.

### Verify MCP Is Loaded

| How to check | Expected result |
| --- | --- |
| Cursor: **Settings → MCP** | `beken_lvgl_ui_designer` is listed and connected |
| TRAE: MCP configuration | `beken_lvgl_ui_designer` is registered and connected |

![Cursor MCP](/doc/images/mcp_status.png)

**If MCP is not loaded:** fully quit Cursor or TRAE, then reopen from the Designer toolbar **AI Design** entry. **Do not** open another folder or a path other than the project's `.ai-workspace` manually.

### Global AI Settings

In **Settings → AI Settings** you can:

- Check Bridge status
- View MCP / Skill install status and versions for each AI tool
- Install, update, or uninstall the AI design environment

> After installing or uninstalling MCP / Skill, **fully quit** the AI tool and reopen it from **AI Design**.

---

## 💬 How to Design with AI

### 1. Launch the AI Tool

Choose an installed AI tool from **AI Design** on the toolbar. Designer ensures MCP / Skill are ready and opens that project's `.ai-workspace`.

### 2. Describe Requirements in Chat

Describe the UI change you want, as you would to a design assistant. Example:

```text
Turn the home page into a device status panel: title at the top, temperature and humidity in the middle, three action buttons at the bottom.
```

**Tips:**

- Name the **page**, **layout**, and content for each area
- Add colors, font sizes, spacing, and other visual details when needed
- **Make one clear change at a time**, review the result, then continue
- Import images or fonts through the [resource manager](workspace-toolbar.md) before asking the AI to use them

### 3. Watch Canvas Feedback

While the AI talks to Designer through MCP, the canvas shows feedback:

| Phase | Canvas behavior |
| --- | --- |
| **Read / analyze** | Scan animation with "AI smart analysis in progress..." |
| **Write / modify** | Animated border around the canvas while changes are applied |

### 4. Confirm or Roll Back Changes

When a round of AI edits finishes, **Save** and **Rollback** appear at the bottom of the canvas:

- **Save** — accept this round of AI changes and add them to undo history
- **Rollback** — restore the state before this round started
- If you **edit manually** or start a **new AI conversation** without choosing, pending changes are **saved automatically**

---

## ✅ Supported Capabilities

Through MCP, the AI can typically:

- Read project summary, page list, and component tree
- Create, delete, and move components
- Update component properties and styles
- Create or switch pages

Some advanced features (complex event chains, fine-grained timeline animation tuning, etc.) may not be supported yet. The AI should explain limits; you can finish those parts manually.

---

## ❓ FAQ

| Issue | What to do |
| --- | --- |
| **AI Design button is disabled** | C or MicroPython preview / compile / run is active. Stop it and try again. |
| **Dropdown shows "Not installed"** | Cursor or TRAE is not installed. Install the AI tool first. |
| **Cannot modify UI / no project open** | Open a project and enter the workspace in Designer, then launch from **AI Design**. |
| **Not in workspace** | Enter the project workspace from the home page; do not stay on the project list. |
| **Workspace mismatch** | The AI chat folder is not this project's `.ai-workspace`. Quit the AI tool and reopen the **current project** from Designer **AI Design**. Do not switch folders or open another project manually. |
| **MCP commands fail in the terminal** | MCP runs inside the AI tool, **not** in the shell. Reload by launching again from **AI Design**. |
| **Still broken after MCP install or update** | Fully quit Cursor or TRAE and reopen from **AI Design**, or uninstall and reinstall MCP under **Settings → AI Settings**. |
| **AI result is not what you wanted** | Click **Rollback** and retry with a more specific prompt (page name, layout, component types, colors). Prefer small steps. |
| **Bridge status is abnormal** | Click **Refresh** under **Settings → AI Settings** and ensure Bridge is running. |

---

## 💡 Best Practices

1. **Always launch from Designer** — keep Designer and the AI tool on the same project
2. **Stay in the workspace** — MCP edits require Designer to be on the workspace screen
3. **Iterate in small steps** — one clear goal per request, then review
4. **Combine with manual editing** — use the [properties panel](workspace-properties.md), [event system](workspace-events.md), and other tools for complex interactions, animation, and i18n
5. **Save the project when it matters** — confirmed AI edits join undo history; 

---

## 🔗 Related Topics

- **[Toolbar](workspace-toolbar.md)** — AI Design entry
- **[Canvas](workspace-canvas.md)** — preview AI changes and the confirm bar
- **[Component Library](workspace-components.md)** — available component types

---

**Workspace Documentation**: [← Back to Workspace](workspace.md) | [Canvas](workspace-canvas.md) | [Components](workspace-components.md) | [Tree](workspace-tree.md) | [Properties](workspace-properties.md) | [Events](workspace-events.md) | [I18n](workspace-i18n.md) | [Timeline Animation](workspace-animation.md) | [AI Design](workspace-ai-design.md) | [Toolbar](workspace-toolbar.md) | [Shortcuts](workspace-shortcuts.md)
