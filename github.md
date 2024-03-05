# GitHub

## URL format for (raw) file contents

GitHub no longer serves file contents as plain HTML on the website. JavaScript
is now required to render them. To get raw file contents without JS, convert the
URL as follows:

```txt
https://github.com/<USER>/<REPO>/blob/<BRANCH>/<PATH>
```

```txt
https://raw.githubusercontent.com/<USER>/<REPO>/<BRANCH>/<PATH>
```

`<PATH>` refers to the full path for a file within subdirectories. Should the
file appear in the base of the repository, the value is just the file name.
