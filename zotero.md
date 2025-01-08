# Zotero

## Lengthen file names in Zotero renamer

Open the `about:config` menu (see 'Zotero Preferences' -> 'Advanced' -> 'Config
Editor') and set `extensions.zotero.attachmentRenameFromString` to
`{%c - }{%y - }{%t{200}}`.

## Use system Firefox when opening snapshots (Zotero 7)

Unset the `MOZ_ALLOW_DOWNGRADE` and `MOZ_LEGACY_PROFILES` environment variables
in the Zotero executable script.

```sh
export MOZ_ALLOW_DOWNGRADE=1
export MOZ_LEGACY_PROFILES=1
```
