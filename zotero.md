# Zotero

## Configure ZotFile

### Location of Files

- Custom location: `${HOME}/Documents/Zotero`
  - Expand `${HOME}` to whatever the value is on your system. The form doesn't
    actually parse shell environment variables.
  - Paths need to be absolute. Relative paths will cause ZotFile's file moving
    operations to break.

### Renaming rules

Format for all Item Types except Patents

```
{%a -}{ %y -}{ %t}
```

- Delimiter between multiple authors: `and`
<!-- - Truncate title after . or : or ? -->
- Maximum length of title: `200`
  - ext4/ntfs max is 255, but leave room for file extensions, etc.
- Maximum number of authors: `2`
- Number of authors to display when authors are omitted: `1`
- Add suffix when authors are omitted: `et al.`

## Rename/move indexed files with ZotFile

1. In the 'My Library' view, highlight all the documents. For simplicity,
   1. Click the topmost entry,
   2. Press `Shift`, and
   3. Press `End`.
2. Right-click the highlighted mass and hover over the 'Manage Attachments'
   section.
3. Select 'Rename and Move' from the pop-up menu.

If 'Attach stored copy of files' is selected in the ZotFile Preferences under
the 'General Settings' tab, then all indexed files will be renamed based on the
relevant metadata.

If 'Custom Location' is specified in ZotFile instead, then all compatible
filetypes (e.g. PDFs) will be moved to the specified directory. Incompatible
types (e.g. HTML snapshots) will be untouched. The attachments in the Zotero
database will be converted to symlinks to the files in the custom location, so
any file name changes or deletions there will break the symlink entries in the
database.

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
