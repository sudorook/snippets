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

## Select the default Firefox profile for opening HTML snapshots

Zotero may create its own profile in ~/.mozilla. In the ~/.mozilla/firefox,
directory, open the profile.ini file and ensure that `Default=1` is applied to
the desired profile.
