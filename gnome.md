# GNOME

## Change font size of GNOME shell

Unlike applications, titlebars, and other components of the UI, the shell font
(e.g. top panel, application launcher menus, etc.) cannot be changed by default.
Font changing can be enabled, though, by overriding the default CSS rules.

1. Enable user themes in the GNOME Tweaks menu.
2. Create a directory `~/.local/share/themes/<theme name>`.
3. Within the `<theme name>` directory, create `gnome-shell/gnome-shell.css`.
4. Edit the `gnome-shell.css` file as follows:

   ```css
   @import url("resource:///org/gnome/theme/gnome-shell.css");

   stage {
     font-size: 10pt;
   }
   ```

5. Select the theme in GNOME Tweaks. It will be under the 'Shell' drop-down menu
   as `<theme name>`. (This requires that user themes is enabled in the
   Extensions applications.

These CSS rules will use the default theme and only apply a change to the font
size attribute. Other style overrides can also be applied this way.

Now, a new option will appear in the Shell drop-down menu in the 'GNOME Tweak ->
Appearance' menu.

Note that this fix will only apply to widgets that follow a global default
styling --- application that use classes with defined font sizes will not be
changed.
