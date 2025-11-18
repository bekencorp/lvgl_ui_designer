# 🎯 Event System

The event system is used to add interactive functionality to components, enabling user interaction with the interface.

## 📍 Accessing the Event Editor

The event editor is located in the **"Events"** tab of the **Properties Panel**:

1. Select the component to which you want to add an event
2. In the right-side properties panel, click the **"Events"** tab
3. You will see the event editor interface

## 🎨 Event System Overview

The event system allows you to configure interactive behaviors for components. When users interact with components (such as clicking, long-pressing, etc.), corresponding actions can be triggered (such as page navigation, property modification, etc.).

### Event System Workflow

```
User Interaction → Trigger Event → Execute Action → Interface Response
```

For example:
- User clicks a button → Triggers `LV_EVENT_CLICKED` event → Executes "Page Navigation" action → Navigates to target page

## ➕ Adding Events

### Step 1: Open the Event Editor

1. Select the component to which you want to add an event
2. Find the **"Events"** tab in the properties panel
3. Click the **"Add Event"** button

### Step 2: Select Event Type

Choose the condition that triggers the event. Common event types include:

**Input Interaction Events**
- **LV_EVENT_CLICKED**: Triggered when the component is clicked (most commonly used)
- **LV_EVENT_DOUBLE_CLICKED**: Triggered when the component is double-clicked
- **LV_EVENT_LONG_PRESSED**: Triggered when the component is long-pressed
- **LV_EVENT_PRESSED**: Triggered when the component is pressed
- **LV_EVENT_RELEASED**: Triggered when the component is released

**Focus Events**
- **LV_EVENT_FOCUSED**: Triggered when the component gains focus
- **LV_EVENT_DEFOCUSED**: Triggered when the component loses focus

**Value Change Events**
- **LV_EVENT_VALUE_CHANGED**: Triggered when the component value changes (e.g., slider movement, input field input)

**Scroll Events**
- **LV_EVENT_SCROLL**: Triggered when the component is scrolled

### Step 3: Select Action Type

Choose the action to execute when the event is triggered:

- **Page Navigation**: Navigate to a specified page
- **Modify Property**: Modify one or more property values of a component
- **Modify Style**: Modify one or more style properties of a component
- **Call Function**: Call a custom function

### Step 4: Configure Action Parameters

Configure the corresponding parameters based on the selected action type:

#### Page Navigation Parameters

**Target Page**
- Select the target page from the dropdown list

**Animation Type**
- **none**: No animation
- **fade_in / fade_out**: Fade in/out effect
- **move_left / move_right / move_top / move_bottom**: Slide effect
- **over_left / over_right / over_top / over_bottom**: Overlay effect
- **out_left / out_right / out_top / out_bottom**: Slide out effect

**Animation Duration**
- Set the animation duration (in milliseconds), default is 300ms

**Animation Delay**
- Set the animation delay time (in milliseconds), default is 0ms

#### Modify Property Parameters

**Target Component**
- Select the component to modify (default is the current component)
- You can select other components in the page from the dropdown list

**Property List**
- Click the **"Add Property"** button
- Select the property to modify (such as Text, Width, Height, etc.)
- Enter the new property value
- You can add multiple property modification items

#### Modify Style Parameters

**Target Component**
- Select the component to modify (default is the current component)

**Style Part**
- Select the style part to modify (such as Main, Indicator, Scrollbar, etc.)

**Style State**
- Select the style state to modify (such as Default, Pressed, Focused, etc.)

**Style Property List**
- Click the **"Add Style Property"** button
- Select the style property to modify (such as background color, font size, border width, etc.)
- Enter the new style property value
- You can add multiple style property modification items

#### Call Function Parameters

**Function Name**
- Enter the name of the function to call (e.g., `handleButtonClick`)

### Step 5: Save Event

1. **Optional**: Add an event description (to explain the event's purpose for future maintenance)
2. Click the **Confirm** button to save the event
3. The event will appear in the event list

## ✏️ Editing Events

### Edit Existing Event

1. Click the event you want to edit in the event list
2. Modify the event type, action type, or parameters
3. Click the **Confirm** button to save the changes

### Delete Event

There are two ways to delete an event:

**Method 1: Delete from Event List**
- In the event list, click the **Delete** button on the right side of the event
- Confirm the deletion operation

**Method 2: Delete from Edit Mode**
- Click the event to enter edit mode
- Click the **Delete** button in the edit form header
- Confirm the deletion operation

## 📋 Event List

The event list displays all events of the current component, including:

- **Event Type**: Shows the trigger condition (e.g., CLICKED, LONG_PRESSED)
- **Action Type**: Shows the action to execute (e.g., page navigation, modify property)
- **Description**: Shows the event description (if any)
- **Action Buttons**: Edit, Delete

## 🎯 Event Connection Visualization

In the canvas, you can view the connection relationships between events and target components:

1. In the canvas toolbar's **View** menu, select **Show Event Connections**
2. The canvas will display connections between events and target components
3. Click on a connection to quickly locate the corresponding event configuration

## 🔗 Related Features

- **[Properties Panel](workspace-properties.md)** - The event editor is located in the properties panel
- **[Canvas](workspace-canvas.md)** - View event connections in the canvas
- **[Component Tree](workspace-tree.md)** - Manage component hierarchy relationships

---

**Workspace Documentation**: [← Back to Workspace](workspace.md) | [Canvas](workspace-canvas.md) | [Components](workspace-components.md) | [Tree](workspace-tree.md) | [Properties](workspace-properties.md) | [Events](workspace-events.md) | [Toolbar](workspace-toolbar.md) | [Shortcuts](workspace-shortcuts.md)

