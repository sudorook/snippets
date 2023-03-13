# Cinnamon

## Reduce margin between applications in grouped window list

Change the `this.actor.style` attribute in the `setMargin()` method of the
`AppGroup` class. To reduce the icon margins to 2px, the code will read as:
```js
setMargin() {
  let direction = this.state.isHorizontal ? 'right' : 'bottom';
  let existingStyle = this.actor.style ? this.actor.style : '';
  this.actor.style = existingStyle + 'margin-' + direction + ':2px;';
}
```

The file is located at
`cinnamon/applets/grouped-window-list@cinnamon.org/appGroup.js`.

To all the above in a single command, run:
```js
sudo sed -i \
  "s/this.actor.style = existingStyle + 'margin-' + direction + ':6px;'/this.actor.style = existingStyle + 'margin-' + direction + ':2px;'/g" \
  /usr/share/cinnamon/applets/grouped-window-list@cinnamon.org/appGroup.js
```
