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
return ((taskFrame.margins.left + taskFrame.margins.right) * spacingAdjustment - 2);
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
