# Bash

## Extract substrings from variables

Use `#` and `##` to match from the start of a string and return the shortest and
longest possible match, respectively. Alternatively, use `%` and `%%` for
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

`-v` will cause each command to be echoed before running, and `-x` will echo the
output of each command. This can also be accomplished by setting (`set -vx`)
after the shebang in the script itself.

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

## Process `stdin` in functions

When constructing functions to use as part of a sequence of pipes, one may
require logic that processes standard input.

To iterate over each line of standard input, use:

```bash
while read -r line
  ...
done <<< "$(< /dev/stdin)"
```

Alternatively, to store all the input in a variable, use:

```bash
var=$(< /dev/stdin)
```

To store multiple inputs from stdin as separate entries of an array, run:

```bash
read -r -a var <<< "${@}"
```

**Note:** If the values are newline delimited, use `mapfile -t arr <<< "${@}"`
instead.

## Source scripts without executing

To source a script, for example, to define variables and functions, wrap the
execution logic (that is not to be executed) as follows:

```bash

if [ "$0" = "${BASH_SOURCE[0]}" ]; then
  ...
fi
```

Any code inside the `if` block will only be executed when the script itself is
directly executed.

## Print all ASCII characters in one string

```bash
for ((i=32;i<127;i++)) do printf "\\$(printf %03o "$i")"; done; printf "\n"
```

## Parallelize a `for` loop

To quickly parallelize a `for` loop, use a counter, `&`, and `wait` to run up to
`N` commands at once. Run:

```bash
N="$(nproc)"
i=0
for ...; do
  <command> &
  i=$((i+1))
  if [ $((i%N)) -eq 0 ]; then
    i=0
    wait
  fi
done
wait
```

## Run command shadowed by alias

Either specify the absolute path or use `command`:

```sh
command <cmd>
```

## Delete entry of an array

To delete a value from a Bash array, use `unset` as follows:

```bash
unset arr[0]
```

The above command removes the `0`th element of an array called `arr`. Note that
the indices of the array do not change (i.e. the `1`st element is not re-indexed
to the `0`th).

Should resetting indices be necessary, a new array needs to be created. Use:

```bash
unset arr[0]
arr=(${arr[@])
```
