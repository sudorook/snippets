# tar

## Compress remote file / directory over SSH and store locally

```sh
ssh <user>@<host> "tar cf - <dir>" | zstd > <archive>
```

## Manually set the decompression program

When extracting a compressed tar archive, `tar` will automatically pick the
decompression program. Should one want to override the default behavior and
manually specify the program, use:

```sh
tar --use-compress-program=<program> -xf <input>
```

For example, `zstd`-compressed tar archive can be decompressed by
`--use-compress-program=unzstd`.
