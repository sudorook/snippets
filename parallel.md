# parallel

## Execute function over Bash array

```sh
parallel <function> ::: <array>
```

`<function>` is a pre-defined shell function (be sure to `export -f <function>`
beforehand), and `<array>` is a fully dereferenced (i.e. `${...[@]}` array.
