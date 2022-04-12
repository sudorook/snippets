# Bash

## Extract substrings from variables

Use `#` and `##` to match from the start of a string and return the shortest
and longest possible match, respectively. Alternatively, use `%` and `%%` for
matching from the end of strings. After expansion, what is returned is the
remaining portions of the string that were unmatched.

To illustrate, the following (result in comment):
```bash
var="one.two.three.four"
${var}     # one.two.three.four
${var#*.}  # two.three.four
${var##*.} # four
${var%.*}  # one.two.three
${var%%.*} # one
```

## Capitalize

```bash
${var,,pattern} # lowercase all
${var,pattern}  # lowercase first letter
${var^^pattern} # uppercase all
${var^pattern}  # uppercase first letter
```

If `pattern` is unspecified, all possible characters to convert will be
converted.

When applied to an array (subscripted by `[@]` or `[*]`, the pattern is applied
to each item. Items are then returned as a list.

An alternate method is to use the `@` and an operator:
```bash
${var@U} # all uppercase
${var@u} # 1st character uppercase
${var@L} # all lowercase
```

## Check if a file is empty

```bash
[ -s <file> ]
```

## Check if an inode is readable

```bash
[ -r <file> ]
```

## Logging output of a bash script

Rather than embed `echo` in several places of a script, run:
```bash
sh -vx <script>
```

`-v` will cause each command to be echoed before running, and `-x` will echo
the output of each command. This can also be accomplished by setting (`set
-vx`) after the shebang in the script itself.

Add the `-n` flag check syntax without executing the script.

## Prevent interrupt

To prevent the user from interrupting a process, add:
```bash
trap '' 2
```

The signal `2` corresponds to user interrupt (`CTRL+C`). To undo this and
re-enable interrupts, use:
```bash
trap 2
```

These two invocations can be used to prevent a sensitive section of code from
being interrupted.
