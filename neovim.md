# Neovim

## Disable mouse

```vim
set mouse=
```

## Set Neovim as default merge and diff tool in Vim

In the local .git/config or global ~/.gitconfig file, set:

```txt
[diff]
  tool = nvimdiff
[merge]
  tool = nvimdiff
```

Other options with different default layouts are available. From
`git mergetool --tool-help`, run:

```txt
nvimdiff         Use Neovim with a custom layout (see `git help mergetool`'s `BACKEND SPECIFIC HINTS` section)
nvimdiff1        Use Neovim with a 2 panes layout (LOCAL and REMOTE)
nvimdiff2        Use Neovim with a 3 panes layout (LOCAL, MERGED and REMOTE)
nvimdiff3        Use Neovim where only the MERGED file is shown
```

## Force default formatexpr behavior

```vim
:lua vim.bo[0].formatexpr = nil
```

## Generate diff of two existing splits

To generate a diff view of two different, vertically split buffers, enter the
command:

```vim
:windo diffthis
```

## Exit edit mode in Neovim terminal when in tmux

In tmux, it is not possible to exit edit mode in a Neovim terminal using `Esc`.
To exit, instead enter:

```
<CTRL+\+n>
```

Note this is a keyboard shortcut, not something to be entered in command mode.
