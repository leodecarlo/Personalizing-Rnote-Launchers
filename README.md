# Personalizing-Rnote-Launchers

Customize your Rnote experience with these keyboard shortcuts to improve your note-taking workflow. This repository provides instructions for setting up three essential shortcuts that let you control Rnote directly from your keyboard.

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

  - Command: ```gdbus call --session --dest com.github.flxzt.rnote --object-path /com/github/flxzt/rnote --method com.github.flxzt.rnote.AddPage```
  - Function: Creates a new blank page in your current Rnote document
  - Default Shortcut: Ctrl + Alt + +
  - Use Case: When you need to quickly add more space for your notes without interrupting your flow

### 2. Export Shortcut
  
  - Command: ```gdbus call --session --dest com.github.flxzt.rnote --object-path /com/github/flxzt/rnote --method com.github.flxzt.rnote.Export``
  - Function: Exports your current document to your default export format
  - Default Shortcut: Ctrl + E
  - Use Case: When you need to quickly save your work in a different format (PDF, SVG, etc.)

### 3. Remove Page Shortcut
  
  - Command: gdbus call --session --dest com.github.flxzt.rnote --object-path /com/github/flxzt/rnote --method com.github.flxzt.rnote.RemovePage
  - Function: Removes the currently selected page from your document
  - Default Shortcut: Ctrl + Alt + -
  - Use Case: When you need to clean up your document by removing unwanted pages

## Prerequisites
  - Rnote must be installed on your system
  - Your desktop environment must support custom keyboard shortcuts
  - Rnote must be running when you use these shortcuts (they won't launch Rnote)

## Installation

No installation is needed for the shortcuts themselves. You just need to configure them in your system settings.

## Setup Instructions

### For GNOME:

- Open *Settings > Keyboard Shortcuts*
- Click *+* to add a custom shortcut
- Fill in the details:
    - Name: [Choose one of the three names shown in screenshots]
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

### For Other Desktop Environments:
The process is similar - look for "Custom Shortcuts" or "Keyboard Shortcuts" in your system settings.

## Troubleshooting
- Shortcut doesn't work: Make sure Rnote is running before using the shortcut
- Command not found: Verify you have ```gdbus``` installed (part of ```glib2``` or similar package)
- Permission denied: Check that Rnote's D-Bus interface is properly exposed
- No visible effect: The command might be working but the UI doesn't update immediately - try pressing the shortcut again

## Customization

Add additional Rnote commands by exploring its D-Bus interface. To explore available Rnote D-Bus methods:

```bash gdbus introspect --session --dest com.github.flxzt.rnote --object-path /com/github/flxzt/rnote ```

## Note
The exact D-Bus method names may vary depending on your Rnote version. If the commands don't work, you may need to adjust the method name based on your specific Rnote installation.

*This repository provides documentation only - no actual code files are included.*


Modifica Immagine

