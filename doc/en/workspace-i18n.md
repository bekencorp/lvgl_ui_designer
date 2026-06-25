# 🌍 I18n (Internationalization)

The I18n feature allows you to configure multi-language support for your project, enabling internationalization of interface text. Through the I18n feature, you can provide different text content and font schemes for different languages.

## 📍 Accessing I18n Configuration

The I18n configuration is located in the **"I18n"** tab of the **Asset Manager**:

1. In the toolbar, click the **"Assets"** button
2. In the Asset Manager dialog, click the **"I18n"** tab
3. You will see the I18n configuration interface

> **Note**: Before using the I18n feature, you need to enable it in the project settings first.

---

## 🚀 Quick Start

### Step 1: Enable I18n in Project Settings

1. In the toolbar, click the **"Settings"** button (or use the shortcut)
2. In the Project Settings dialog, find the **"Internationalization"** section
3. Enable the **"Multi-language"** switch
4. Click the **"Close"** button to save the settings

![Enable I18n in Project Settings](/doc/images/i18n-project-settings.png)

> **Tip**: After enabling I18n, the "I18n" tab in the Asset Manager will display the configuration interface.

---

## 📚 I18n Configuration

The I18n configuration consists of three main parts:

### 1. Language Management

Used to manage the list of supported languages and default language settings.

#### Adding a Language

1. In the "Languages" tab, click the **"Add Language"** button
2. In the Add Language dialog:
   - **Language Code**: Select or enter a language code (e.g., `zh_CN`, `en_US`)
   - **Default Font**: Select the default font for this language
3. Click the **"Confirm"** button to add the language

![Add Language](/doc/images/i18n-add-language.png)

> **Tips**:
> - When adding the first language, the system will automatically set it as the default language
> - Language codes are used to identify languages. It is recommended to use standard formats (e.g., `zh_CN`, `en_US`)

#### Setting Default Language

1. In the "Languages" tab, find the **"Default Language"** dropdown
2. Select the language to set as default from the dropdown list
3. The default language will be saved automatically

![Set Default Language](/doc/images/i18n-default-language.png)

#### Deleting a Language

1. In the language list, find the language you want to delete
2. Click the **"Delete"** button on the right side of the language row
3. Confirm the deletion operation

> **Note**: Deleting a language will also delete all translation content for that language. Please proceed with caution.

---

### 2. Text Translation

Used to manage all text content that needs translation and translations for each language.

#### Adding a Translation Key

1. In the "Text Translation" tab, click the **"Add Text"** button
2. In the Add Text dialog, enter a translation key (e.g., `welcome_text`, `button_ok`)
3. Click the **"Confirm"** button to add
4. In the multi-language table, add translations for the key in corresponding languages

![Add Translation Key](/doc/images/i18n-add-text.png)
![Add Translation Key](/doc/images/i18n-add-text-lan.png)

> **Tips**:
> - Translation keys should use meaningful names for easier maintenance
> - It is recommended to use underscore naming (e.g., `welcome_text`, `button_ok`)

#### Editing Translation Content

1. In the translation list, find the translation key you want to edit
2. Click the translation content in the corresponding language column (or click the **"Edit"** button)
3. In the Edit Translation dialog, enter the translation text for that language
4. Click the **"Confirm"** button to save

![Edit Translation](/doc/images/i18n-edit-translation.png)

> **Tips**:
> - You can set different translation content for each language
> - If a language has no translation, it will display as empty or use the default language translation

#### Editing Translation Key

1. In the translation list, find the translation key you want to edit
2. Click the content in the Key column (or click the **"Edit"** button)
3. In the Edit Key dialog, modify the key name
4. Click the **"Confirm"** button to save

> **Note**: Modifying the key name will affect all components using that key. Please proceed with caution.

#### Deleting Translation Key

1. In the translation list, find the translation key you want to delete
2. Click the **"Delete"** button on the right side of the key row
3. Confirm the deletion operation

> **Note**: Deleting a translation key will also delete all translation content for all languages. Please proceed with caution.

---

### 3. Language Font Schemes

Used to manage font schemes corresponding to different languages, enabling automatic font switching by language.

#### Adding Font Scheme

1. In the "Language Font Schemes" tab, click the **"New Scheme"** button
2. In the Add Scheme dialog, enter a scheme name (e.g., `scheme_chinese`, `scheme_english`)
3. Click the **"Confirm"** button to add the scheme

![Add Font Scheme](/doc/images/i18n-add-font-scheme.png)

> **Tips**:
> - Scheme names can only contain letters, numbers, and underscores
> - Scheme names cannot be the same as font names

#### Configuring Language Font Mapping

1. In the font scheme list, find the scheme you want to configure
2. In the dropdown for the corresponding language column, select the font to use for that language
3. You can also select **"Inherit"** to use the default scheme's font settings

![Configure Language Font Mapping](/doc/images/i18n-font-mapping.png)

> **Tips**:
> - You can set different fonts for each language
> - When selecting "Inherit", the default scheme's font settings will be used
> - If a language has no font set, the default font will be used

#### Editing Font Scheme

1. In the font scheme list, find the scheme you want to edit
2. Click the **"Edit"** button on the right side of the scheme row
3. In the Edit Scheme dialog, modify the scheme name
4. Click the **"Confirm"** button to save

#### Copying Font Scheme

1. In the font scheme list, find the scheme you want to copy
2. Click the **"Copy"** button on the right side of the scheme row
3. The system will automatically create a new scheme with the name format `original_scheme_name_copy`

#### Deleting Font Scheme

1. In the font scheme list, find the scheme you want to delete
2. Click the **"Delete"** button on the right side of the scheme row
3. Confirm the deletion operation

> **Note**: Deleting a font scheme will affect components using that scheme. Please proceed with caution.

---

## 🎨 Using I18n in Projects

### Example 1: Enable Translation for Label Component Text

#### Step 1: Add Label Component

1. In the component library, find the **"Label"** component
2. Drag the Label component onto the canvas
3. Select the Label component

#### Step 2: Enable Text Translation

1. In the Properties Panel, find the **"Properties"** tab
2. Expand the **"Properties"** group and find the **"Text"** property
3. Click the **"Enable Translation"** button (or toggle switch) on the right side of the Text property input
4. Enter a translation key (e.g., `welcome_text`)

![Label Enable Translation](/doc/images/i18n-label-enable-translation.png)

> **Tips**:
> - After enabling translation, the entered content will be used as the I18n key
> - If the key does not exist, the system will prompt you to add a translation

#### Step 3: Select Font Scheme

1. In the Properties Panel, in the **"Style"** tab
2. Expand the **"Font"** style group
3. In the **"Font"** property, select the font scheme to use

![Label Select Font Scheme](/doc/images/i18n-label-font-scheme.png)

> **Tips**:
> - After selecting a font scheme, the font will automatically switch based on the current language
> - If no scheme is selected, the default font will be used

---

### Example 2: Enable I18n for Button Component Event Action

#### Step 1: Add Button Component

1. In the component library, find the **"Button"** component
2. Drag the Button component onto the canvas
3. Select the Button component

#### Step 2: Add Click Event

1. In the Properties Panel, switch to the **"Events"** tab
2. Click the **"Add Event"** button
3. Select event type: **"LV_EVENT_CLICKED"**
4. Select action type: **"Modify Property"**

#### Step 3: Configure Modify Property Action

1. In the action parameter configuration:
   - **Target Component**: Select the component to modify (e.g., the Label component added earlier)
   - Click the **"Add Property"** button
   - Select the property to modify: **"Text"**
   - In the property value input, click the **"Enable Translation"** button
   - Enter a translation key (e.g., `button_clicked_text`)

![Button Event I18n](/doc/images/i18n-button-event-translation.png)

#### Step 4: Add Translation Content

1. If the key does not exist, follow Step 2 of Example 1 to add translation content
2. Set different translation text for different languages

---

### Example 3: Switch Language Event

The switch language event allows users to dynamically switch the display language of the project by clicking a button or other interactive methods.

#### Step 1: Add Button Component

1. In the component library, find the **"Button"** component
2. Drag the Button component onto the canvas
3. Select the Button component

#### Step 2: Add Click Event

1. In the Properties Panel, switch to the **"Events"** tab
2. Click the **"Add Event"** button
3. Select event type: **"LV_EVENT_CLICKED"**
4. Select action type: **"Switch Language"**

> **Note**: The "Switch Language" action type will only appear in the action list after I18n is enabled in the project settings.

#### Step 3: Configure Switch Language Parameters

1. In the action parameter configuration:
   - **Target Language**: Select the language to switch to from the dropdown list (e.g., `zh_CN`, `en_US`)
   - **Refresh Page**: Choose whether to refresh the page after switching language
     - **Enabled**: After switching language, the current page will be refreshed, and the text in the new language will be displayed immediately
     - **Disabled**: After switching language, the page will not be refreshed, and the text will switch on the next update

![Switch Language Event Configuration](/doc/images/i18n-switch-language-event.png)

> **Tips**:
> - The target language list comes from the languages you added in "Language Management"
> - If no languages are added to the project, the target language list will be empty
> - It is recommended to enable the "Refresh Page" option so users can immediately see the language switch effect

#### Step 4: Test Switch Language Function

1. Save the project and run the preview
2. Click the button configured with the switch language event
3. Observe whether the interface text has switched to the target language

> **Tips**:
> - After switching language, all component text using translation keys will automatically update
> - If components use font schemes, the font will also automatically switch according to the new language
> - You can view the switch language event connection in the canvas, which points to the language block (displayed in the upper right corner of the canvas)

---

## 💡 Usage Tips

### 1. Translation Key Naming Convention

It is recommended to use meaningful naming conventions for easier maintenance:

- **Page-level text**: `page_welcome`, `page_settings`
- **Button text**: `button_ok`, `button_cancel`, `button_save`
- **Label text**: `label_username`, `label_password`
- **Tip text**: `tip_loading`, `tip_success`, `tip_error`

### 2. Font Scheme Management

- **Default Scheme**: Used to set the default font for each language
- **Custom Schemes**: Used for font configuration in special scenarios
- **Inheritance Mechanism**: Custom schemes can choose to inherit the default scheme's font settings

### 3. Translation Preview

In the Properties Panel, after enabling translation, you can view the translation preview:

1. Below the property input, the translation preview for the current language will be displayed
2. If the key does not exist or the translation is empty, a prompt message will be displayed

### 4. Batch Translation Management

In the "Text Translation" tab, you can:

- Use the search function to quickly find translation keys
- Batch edit translation content for multiple languages
- Export/import translation configuration (if supported)

---

## 🔗 Related Features

- **[Properties Panel](workspace-properties.md)** - Enable translation in the Properties Panel
- **[Event System](workspace-events.md)** - Use I18n in event actions
- **[Asset Manager](workspace-toolbar.md#asset-manager)** - Manage I18n configuration
- **[Project Settings](workspace-toolbar.md#project-settings)** - Enable I18n feature

---

**Workspace Documentation**: [← Back to Workspace](workspace.md) | [Canvas](workspace-canvas.md) | [Components](workspace-components.md) | [Tree](workspace-tree.md) | [Properties](workspace-properties.md) | [Events](workspace-events.md) | [Timeline Animation](workspace-animation.md) | [AI Design](workspace-ai-design.md) | [Toolbar](workspace-toolbar.md) | [Shortcuts](workspace-shortcuts.md)

