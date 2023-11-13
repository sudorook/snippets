# kitty

## Add a kitty terminfo config to a remote server

```sh
infocmp -x xterm-kitty | ssh <server> tic -x -o \~/.terminfo /dev/stdin
```

`tic` is the TermInfo Compiler, and `infocmp` is for printing the kitty terminfo
(`xterm-kitty`) to stdout.

## List available fonts

```sh
kitty +list-fonts --psnames
```

## Enable scrollback of history

To enable scrollback, enter `<CTRL+SHIFT+H>` in the terminal. By default, kitty
will use `less` for the pager, but changing the `scrollback_pager` in
`kitty.conf` option allows for alternate programs.

To increase the number of lines available to the pages, edit the kitty.conf as
follows:

```kitty
scrollback_pager_history_size	<size>
```

The `<size>` is in Mb, where 1 Mb yields >10000 lines in the scrollback buffer.
