# cp

## Copy directory and file structure without any file contents

To mirror the entire directory structure of one path to another, run:

```sh
cp -r --attributes-only <source> <dest>
```

All of the files created in the `<dest>` path will be empty.
