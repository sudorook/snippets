# Cinnamon

## Reduce margin between applications in grouped window list

Change the `setMargin()` method in the AppGroup class to read:
```
setMargin() {
  let direction = this.state.isHorizontal ? 'right' : 'bottom';
  let existingStyle = this.actor.style ? this.actor.style : '';
  this.actor.style = existingStyle + 'margin-' + direction + ':2px;';
}
```

The file is located at
`cinnamon/applets/grouped-window-list@cinnamon.org/appGroup.js`.
