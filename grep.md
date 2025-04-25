# grep

## Print file names along with regex matches

```sh
grep -H ...
```

Useful when running `grep` recursively via `-R` or as the `-exec` argument for
`find`.

## Use multiple regex patterns at once

To specify multiple patterns, use logical OR (`|`):

```sh
grep -E `<pattern1>|<pattern2>'
```

Alternatively, use:

```sh
grep -e '<pattern1>' -e '<pattern2>'
```
