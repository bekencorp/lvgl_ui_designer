# ⏱️ Timeline Animation

Timeline animation is used to manage how component properties change over time. You can define animation tracks and keyframes in the timeline editor, then trigger playback at runtime through the event system.

---

## 📍 Entry Location

1. In the workspace main view, look at the bottom **tab bar**
2. Click the **"Animation"** tab (to the right of the **"Log"** tab)
3. After opening the **Timeline Animation** editor, create an animation and select a preview test component

![Animation Entry](/doc/images/animation_tab.png)

---

## 1. 🔑 Key Concepts

### Animation

- An animation is an independent track that includes a name, test component, and multiple keyframes.
- A project can contain multiple animations, and you can choose which one to trigger in events.

### Keyframe

- A keyframe represents the target state at a specific timestamp (ms).
- At least one keyframe can create a visible transition (from current/initial state to that keyframe). Multiple keyframes can define richer continuous changes.

### Property State

- Each keyframe can include selected properties participating in animation (such as `width`, `height`, `bg_color`, `opa`).
- Unselected properties will not participate in keyframe calculation.

### Read Component State

- **Read** writes the **current state of the preview test component** into the selected properties of the current keyframe.
- This is useful when you first adjust the component to the target look on canvas, then write it back to the keyframe in one click.
- It is recommended to select the properties first before reading, to avoid overriding unrelated fields.

### Easing

- Easing controls the speed curve when a property transitions from the previous keyframe to the current keyframe.
- Common types include: linear, ease in, ease out, ease in out, overshoot, bounce.

### Preview Test Component vs Trigger Target Component

- **Preview test component**: only used for preview in the editor.
- **Trigger target component**: the component that actually runs the animation at runtime, configured in the **Trigger Animation** event.
- They can be the same, or different (for example, reusing one animation template for multiple components).

---

## 2. 🧪 Example: Square Scales Up, Then Changes from Red to Blue

The following example creates a square animation that scales from `50x50` to `100x100`, then changes from red to blue.

### Step 1: Prepare a Test Component

1. Add a container component on canvas.
2. Set initial size to `50 x 50` and initial color to red.
3. Name the component (example: `square_1`) for later event targeting.

![Page](/doc/images/animation_setup.png)

### Step 2: Create an Animation Track

1. Open **Timeline Animation**.
2. Click **"Add Animation"**.
3. Set animation name to `square_pulse_color`.
4. Select `square_1` as the preview test component.

![Add Animation](/doc/images/animation_add.png)

### Step 3: Add Keyframes

This example only needs 2 keyframes (initial state uses the current component state directly, so no extra initial keyframe is needed):

- `500ms`: complete scaling (`100 x 100`), keep red color
- `1000ms`: keep size at `100 x 100`, and transition color from red to blue

![Timeline](/doc/images/animation_timeline.png)

### Step 4: Configure Keyframe Properties

#### Keyframe A (500ms)

- `width = 100`
- `height = 100`
- `bg_color = red`

#### Keyframe B (1000ms)

- `width = 100`
- `height = 100`
- `bg_color = blue`

Suggested easing:

- To `500ms`, use **ease out**

### Step 5: Preview and Fine-tune

1. Click **"Preview"** to play the animation.
2. Check whether the sequence "scale first, then color change" matches expectations.

![Page](/doc/images/animation_preview.gif)

---

## 3. 🎯 How to Trigger Animation on Screen Load

After defining timeline animation, trigger it through the event system.

### Step 1: Select Screen (Page) as Trigger Source

1. Back in workspace, select the root node (screen) of the current page in the component tree.
2. Switch to the **Events** tab in the properties panel.

### Step 2: Add Event and Choose Action

1. Click **"Add Event"**.
2. Set event type to `LV_EVENT_SCREEN_LOADED` (triggered when page loading is complete).
3. Set action type to **"Trigger Animation"**.

### Step 3: Configure Trigger Animation Parameters

1. **Animation**: select `square_pulse_color`
2. **Target Component**: select `square_1`
3. **Repeat Count**:
   - `1` means play once
   - `0` means infinite loop
4. **Reverse**: enable as needed (for reverse playback)

![Event](/doc/images/animation_event.png)

### Step 4: Validate Runtime Result

1. Save project and run preview.
2. After page load completes, check whether animation starts automatically.
3. Confirm `square_1` executes "scale first, then change from red to blue" according to timeline.

![Page](/doc/images/animation_run.gif)

---

## 🔗 Related Features

- **[Event System](workspace-events.md)** - configure trigger animation events
- **[Properties Panel](workspace-properties.md)** - view and adjust base component properties
- **[Canvas Area](workspace-canvas.md)** - view the bottom tab bar and switch to the Animation tab

---

**Workspace Documentation**: [← Back to Workspace](workspace.md) | [Canvas](workspace-canvas.md) | [Components](workspace-components.md) | [Tree](workspace-tree.md) | [Properties](workspace-properties.md) | [Events](workspace-events.md) | [I18n](workspace-i18n.md) | [Timeline Animation](workspace-animation.md) | [Toolbar](workspace-toolbar.md) | [Shortcuts](workspace-shortcuts.md)
