# kitty

## Add a kitty terminfo config to a remote server

```
infocmp -x xterm-kitty | ssh <server>  tic -x -o \~/.terminfo /dev/stdin
```

`tic` is the TermInfo Compiler, and `infocmp` is for printing the kitty
terminfo (`xterm-kitty`) to stdout.
