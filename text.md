# Text

## Convert DOS to Unix format

To convert from `dos` to `unix` format, run:
```sh
dos2unix <file>
```

This fixes issues with CRLF line terminators.

## Remove trailing whitespace from all files

```sh
find . -type f -not -path "*/.git/*" -exec sed -i "s/ \+$//g" {} +
```

The `-not -path "*/.git/*"` is to prevent sed from mangling the git history if
present.

## Watch files

To watch the contents of a text file, for example a log file, for newly
appended data, run:
```sh
tail -f <log file>
```
