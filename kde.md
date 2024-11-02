# KDE Plasma

## Horizontally / vertically maximize windows

To horizontally maximize, right-click the 'Maximize' button.

To vertically maximize, left-click the 'Maximize' button.

## Reduce width of icons in Icons-only Task Manager

Icons that are more tall than wide can create the illusion that the application
icons are too widely spaced.

To manually reduce the icon width, reduce the `horizontalMargins()` function in
`/usr/share/plasma/plasmoids/org.kde.plasma.taskmanager/contents/ui/code/layout.js`
as follows:

```js
return (
  (taskFrame.margins.left + taskFrame.margins.right) * spacingAdjustment - 2
);
```

`taskFrame.margins.left` and`taskFrame.margins.right` are global settings with
minimum value of 2. The `spacingAdjustment` variable is a scaling factor of 0,
1, or 3 from the 'Small', 'Medium', or 'Large' combo-box in the 'Configure
Icons-only Task Manager...' menu.

## Disable 'Downloads'-directory date sections in Dolphin

Open 'View' (`CTRL+m`, if top bar is disabled), and uncheck the 'Show in Groups'
checkbox.

## Close active window via keyboard

To close the currently focused window, enter `Alt+F4`.

## Clear clipboard from the command line

Use `qdbus` to clear the Klipper's clipboard history:

```sh
qdbus org.kde.klipper /klipper org.kde.klipper.klipper.clearClipboardHistory
```

## Fix Dolphin 'Empty Trash'

If Dolphin's Trash directory view fails to update after clicking 'Empty Trash',
delete the directory entirely:

```sh
rm -rf ~/.local/share/Trash/
```

## Override Dolphin hiding backup files by default

The new default behavior hides \*.bak, \*.sik, \*.old, \*~, and \*% files as if
they were hidden files. To alter this behavior, create a new file association
MIME-type.

1. Open 'System Settings'
2. Open the 'Applications>File Associations' menu.
3. Under 'Known Types' create a new entry called 'x-backup' and copy over all of
   the rules in 'x-trash'.
4. 'Apply' to set the changes. The generated files can be viewed in
   ~/.local/share/mime/

## Kill an open window

1. Enter `Meta+Ctrl+Esc` to open the kill UI. (The target window needs to be
   visible.)
2. Click in the window to close, or hit `Esc` to cancel.
