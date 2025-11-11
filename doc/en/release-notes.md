# Release Notes

This document records all version updates for BEKEN LVGL UI Designer.

---

## Version History

### 1.0.0

- Initial release of the tool, dedicated to providing a free and easy-to-use platform for embedded LVGL design and development


### 1.0.1

#### Features

- Added Flags settings in component properties panel
- Added State setting in component properties panel
- Add the ability to move selected components using directional shortcut keys (↑, ↓, ←, →)
- Arc component now supports setting Arc class style properties
- Added more STATE for component Style

#### Optimizations

- TabView header height now supports minimum value of 0
- Added alignment guides when dragging child components in containers
- Optimized copy-paste logic for child components within containers
- Canvas automatically scales to fit interface size when entering workspace
- Changed project deletion to manual user action to prevent accidental deletion
- Added resource name restrictions and error prompts when selecting resources
- Display default "Not Found" image when image file is not found

#### Bug Fixes

- Fixed issue where code was not cleared on second generation
- Fixed issue where rendering interface would freeze after closing preview
- Fixed issue where example icons were not displayed when creating projects
- Fixed issue where code generation only supported one page
- Fixed issue where child components nested more than 2 levels deep in container components were not displayed in component tree (now supports up to 4 levels of nesting)
- Fixed compilation error when multiple pages use the same component
- Fixed compilation error when deleting a page after designing and compiling two pages

---

