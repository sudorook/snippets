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
