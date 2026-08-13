# 🔧 Custom Code

Besides designing the UI visually, you may need to add your own C or MicroPython logic. The tool offers **two approaches**—pick the one that fits your workflow, and **do not duplicate the same logic in both places**.

---

## ⚖️ 1. What Is the Difference?

| Item | **In-designer custom code** | **External IDE on generated files** |
|------|----------------------------|-------------------------------------|
| **Where to edit** | Properties panel, event editor | Keil, VS Code, etc., open the `beken_generated` folder |
| **Stored in** | Project file (saved with the project) | `.c` / `.h` files on disk |
| **After regenerate** | Re-injected from the project | Only code **inside** `BEKEN_USER_CODE` markers is kept |
| **Best for** | Quick experiments, MicroPython projects | C firmware, SDK integration, complex logic |

**In-designer** has three entry points (all saved in the project):

- **Page custom code** — runs when the page loads
- **Event → Custom code** — runs on click, value change, etc.
- **Event → Call function** — implement in `custom_func.c`, reuse across components

**External IDE** edits exported generated files, but only inside marker comments:

```c
/* BEKEN_USER_CODE_BEGIN implementation */
// Your code here
/* BEKEN_USER_CODE_END implementation */
```

> **Tip**: In the in-app **Code Editor**, generated files are read-only. You can edit `custom_func.c` and files under `custom/`. For `BEKEN_USER_CODE` regions, use an external IDE.

---

## 🎨 2. In-Designer Custom Code

### Page custom code

Use when the page needs extra setup on load.

1. Select the **page (Screen)**
2. Properties panel → **Custom Code** → **Add / Edit**
3. Fill in **#include and variables** (inside `BEKEN_USER_CODE includes` in `page_*_init.c`) and **Implementation** (inside `BEKEN_USER_CODE implementation` in `init_page_xxx()`)

> **Tip**: For C, page custom code shares the same `BEKEN_USER_CODE` markers with external IDE additions; designer content is refreshed on regenerate, hand-written content after it is preserved.

> **Tip**: Supports both **C** and **MicroPython** tabs.

### Event custom code

Use when a button click or value change should run custom logic.

1. Select a component → Properties **Events**
2. Add an event, action type **Custom code**
3. Fill in **#include and variables** / **Implementation**
4. Click **Confirm**

> **Tip**: Event **includes** go under `// custom event code` (outside markers); event **implementation** goes inside the matching `xxx_event_cb()`.

### Call function

Use when several components share the same handler.

1. Event action **Call function**, enter the function name (e.g. `handleButtonClick`)
2. Implement the function in `custom_func.c`

> **Tip**: `custom_func.c` and the `custom/` folder are **not overwritten** on regenerate.

---

## 💻 3. External IDE

For C projects: open **`beken_generated`** (or your configured export path) in Keil, VS Code, etc.

### Steps

1. Find `BEKEN_USER_CODE_BEGIN` / `BEKEN_USER_CODE_END` in the file
2. Write code **only between** those markers, then save
3. Back in the designer, run **Generate code** or **Generate + Build + Run**

### Notes

- Content **outside** the markers is tool-generated and will be overwritten on regenerate
- After editing `beken_generated`, run **Generate + Build + Run** for the simulator to pick up changes (build alone is not enough)
- When appending code inside markers in `page_*_init.c`, write **after** page property custom code; a blank line in between is recommended

### Editable regions by file

Hand-written C inside `BEKEN_USER_CODE` markers is kept on regenerate; content outside is tool-generated.

| File | Marker slots | Typical use |
|------|--------------|-------------|
| `page_*_init.c` | `includes`, `implementation`, **`file_tail`** | Page headers/vars; logic in `init_page_xxx()`; **append at file end** |
| `beken_ui.c` | `includes`, `implementation`, **`file_tail`** | UI init in `beken_ui_init()`; **append at file end** |
| `beken_ui.h` | `includes` | Headers and declarations |
| `event_runtime.c` | `includes`, `navigate_hook`, `switch_locale_hook`, **`file_tail`** | Navigation/locale hooks; **append at file end** |
| `event_runtime.h` | `includes` | Headers and declarations |
| `lv_i18n.c` | `includes`, `init_hook`, `set_locale_hook`, **`file_tail`** | i18n extensions; **append at file end** (when i18n enabled) |
| `lv_i18n.h` | `includes` | Headers and declarations |
| `basic_callback.c` | `includes`, **`file_tail`** | Headers/vars; **append at file end** |

These paths are **whole files** user-maintained and **not overwritten** on regenerate:

- `custom_func.c` / `custom_func.h` — call-function event handlers
- `custom/` folder — user-added `.c` / `.h`

**Do not edit manually** (overwritten every regenerate):

- `fonts/*.c`, `basic_callback.c`
- Tool-generated sections outside markers

> **Tip**: Search for `BEKEN_USER_CODE` in a file to find preserved hand-written regions.

---

## 🔗 Related

- **[Event System](workspace-events.md)**
- **[Toolbar](workspace-toolbar.md)**
- **[Getting Started](getting-started.md)**

---

**Workspace docs**: [← Back to workspace](workspace.md) | [Events](workspace-events.md) | [Toolbar](workspace-toolbar.md)
