# Personalizing-Rnote-Launchers

Customize your Rnote experience with these keyboard shortcuts to improve your note-taking workflow. This repository provides instructions for setting up three  shortcuts that let you control Rnote directly from your keyboard.

## Features

- Add new pages instantly without navigating menus
- Export notes with a single key combination
- Remove pages efficiently during editing
- Works with Rnote's D-Bus interface for direct application control
- Compatible with GNOME, KDE, and other major desktop environments

## How These Shortcuts Work

Rnote exposes a D-Bus interface that allows external programs to control it. These shortcuts use ```gdbus``` (the GNOME D-Bus client) to send commands to Rnote's service. When you press the configured keyboard combination, the system sends a D-Bus message to Rnote, which then executes the corresponding action.

The commands follow this pattern:

```bash
gdbus call --session --dest com.github.flxzt.rnote --object-path /com/github/flxzt/rnote --method com.github.flxzt.rnote.[Action]
```


## The Three Shortcuts

### 1. Add Page Shortcut

  - Command: ```gdbus call --session --dest com.github.flxzt.rnote --object-path /com/github/flxzt/rnote/window/1 --method org.gtk.Actions.Activate add-page-to-doc "[]" "{}"```
  - Function: Creates a new blank page in your current Rnote document
  - Default Shortcut: Ctrl + Alt + +

### 2. Remove Page Shortcut
  
  - Command: ```gdbus call --session --dest com.github.flxzt.rnote --object-path /com/github/flxzt/rnote/window/1 --method org.gtk.Actions.Activate remove-page-from-doc "[]" "{}"```
  - Function: Removes the currently selected page from your document
  - Default Shortcut: Ctrl + Alt + -

### 3. Export Shortcut
  
  - Command: ```gdbus call --session --dest com.github.flxzt.rnote --object-path /com/github/flxzt/rnote/window/1 --method org.gtk.Actions.Activate export-doc "[]" "{}"```
  - Function: Exports your current document to your default export format
  - Default Shortcut: Ctrl + E

### 4. Selector 
  
  - Command: ```gdbus call --session --dest com.github.flxzt.rnote --object-path /com/github/flxzt/rnote/window/1 --method org.gtk.Actions.Activate pen-style "[<@s 'selector'>]" "{}"```
  - Function: switch to defualt Selector frame
  - Default Shortcut: Ctrl + W

### 5. Shaper 
  
  - Command: ```gdbus call --session --dest com.github.flxzt.rnote --object-path /com/github/flxzt/rnote/window/1 --method org.gtk.Actions.Activate pen-style "[<@s 'shaper'>]" "{}"```
  - Function: switch to defualt Shaper shape
  - Default Shortcut: Ctrl + Q

### 5. Typewriter
  
  - Command: ```gdbus call --session --dest com.github.flxzt.rnote --object-path /com/github/flxzt/rnote/window/1 --method org.gtk.Actions.Activate pen-style "[<'typewriter'>]" "{}"```
  - Function: switch to defualt Typewriter to type
  - Default Shortcut: Ctrl + T

## Setup Instructions

### For GNOME:

- Open *Settings > Keyboard Shortcuts*
- Click *+* to add a custom shortcut
- Fill in the details:
    - Name: 
    - Command: [Use the specific command for that shortcut]
    - Shortcut: [Press your desired key combination]
- Click Add

### For KDE:

- Open System *Settings > Shortcuts*
- Click Custom Shortcuts
- Right-click and select *New > Global Shortcut > Command/URL*
- Configure:
  - Trigger: Set your keyboard shortcut
  - Action: Enter the corresponding command
  - Comment: Add a description
- Click Apply


## Customization

You can create custom shortcuts for almost any feature in Rnote by calling the specific *Action Name* through D-Bus.

To see a list of all available actions (like `undo`, `redo`, `zoom-in`, etc.) for the current window, run tis command while Rnote is open:

```bash
gdbus introspect --session --dest com.github.flxzt.rnote --object-path /com/github/flxzt/rnote/window/1
```

### Constructing a Command
Once you find an action name (e.g., undo), follow this pattern to create the command:

```bash
gdbus call --session --dest com.github.flxzt.rnote --object-path /com/github/flxzt/rnote/window/1 --method org.gtk.Actions.Activate "undo" "[]" "{}"
```

Common parameter types:
  - Simple actions: Use "[]" "{}" (e.g., Undo, Redo).

  - State actions: require parameters inside the brackets, like "[<@s 'selector'>]" for tool switching.

