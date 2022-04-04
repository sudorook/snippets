# Bash

## Check if a file is empty

```sh
[ -s <file> ]
```

## Check if an inode is readable

```sh
[ -r <file> ]
```

## Logging output of a bash script

Rather than embed `echo` in several places of a script, run:
```
sh -vx <script>
```

`-v` will cause each command to be echoed before running, and `-x` will echo
the output of each command. This can also be accomplished by setting (`set
-vx`) after the shebang in the script itself.

Add the `-n` flag check syntax without executing the script.

## Prevent interrupt

To prevent the user from interrupting a process, add:
```
trap '' 2
```

The signal `2` corresponds to user interrupt (`CTRL+C`). To undo this and
re-enable interrupts, use:
```
trap 2
```

These two invocations can be used to prevent a sensitive section of code from
being interrupted.
