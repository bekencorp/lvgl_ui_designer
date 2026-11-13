# Built-in Tools

Built-in tools ship with the application and need no installation. Every tool can also be launched from the workspace toolbar. For each tool's full interface, parameters, and troubleshooting, press **F1** inside its window.

---

## 🧰 Tool Overview

### Project-Linked Tools

These tools can be launched from the workspace and read or write current project data. **Animation Effects Library** can also be opened from the canvas or component tree context menu.

| Tool | Purpose |
| --- | --- |
| **Component Style Gallery** | Browse multiple styles and true renderings for 32 component types, and add a preset to the current canvas in one click |
| **Animation Effects Library** | Add entrance, exit, emphasis, loop, interaction, and value animation presets to components; writes to the timeline for further tuning |
| **Event and Navigation Map** | Summarizes page navigation, component events, and animation triggers, and flags orphan events, dead links, loops, and unbound actions |
| **Resource Budget Analyzer** | Scans the component tree, images, and fonts to estimate Flash / RAM usage, with suggestions for `LV_MEM_SIZE`, image color depth, and font grades |

### Standalone Tools

These tools do not depend on a project and run directly in the Toolbox.

| Tool | Purpose |
| --- | --- |
| **LVGL Image Converter** | Converts PNG / JPG / BMP / WebP into LVGL resources (C source or BIN), with LVGL 8.x / 9.x, multiple color formats, and byte order support |
| **Image Format Converter** | Batch converts PNG / JPG / WebP / BMP with quality control, scale, crop, transparency fill, and size statistics |
| **Font Converter** | Converts TTF / OTF into LVGL bitmap fonts, subsets by the characters actually used, and compares sizes across BPP options |

---

## 🚀 Typical Workflows

### Convert Images to LVGL Resources

1. Open **LVGL Image Converter**
2. Choose the LVGL version, color format, byte order, and output format
3. Add images or a whole folder, then scale, crop, or rotate as needed
4. Export C source or BIN and add it to your project resources

### Use the Component Style Gallery

1. Open a project and enter the workspace
2. Launch **Component Style Gallery** from the workspace toolbar
3. Pick a component category and style to view the true rendering
4. Click **「Add to Current Canvas」** to insert the component with that style

### Add an Animation to a Component

1. Open **Animation Effects Library** and choose an effect to preview
2. Adjust duration, delay, easing, and other parameters
3. Select the target component and click **「Add to Project」**
4. Fine-tune keyframes in the timeline editor

> Image and font tools do not depend on a project and can be used standalone in the Toolbox.

---

**Related:** [Toolbox and Plugins](toolbox.md) | [Build Tools with AI](toolbox-ai-dev.md)
