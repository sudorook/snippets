# Zsh

## Restore missing history from memory

When RAM usage increases, an idle `zsh` can get its history dropped from memory.
If re-engaged, new commands will cause the partially-dropped history to be
written to the '.zsh_history' file. Any new shell will then have a largely
missing command history.

Should truncation occur, it is possible to restore the written Zsh history from
memory using another Zsh shell, ideally one that was running a process
throughout the interval of high memory usage (e.g. `top`). Such processes are
unlikely to have their resources dropped by the scheduler. Run:

```zsh
fc -W ~/zsh_history_from_ram
```

Compare the resulting file with the '.zsh_history' file.
