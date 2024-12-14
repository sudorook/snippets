# C++

## De-mangle C++ symbol names

```sh
c++filt <SYMBOL>
```

## Detect if a binary was compiled with debug symbols

Use either `objdump` (from `binutils`) or `file` (from `coreutils`) to detect if
a binary `<file>` has debug symbols.

```sh
objdump -x <file> | grep \.debug
```

```sh
file <file> | grep debug_info
```
