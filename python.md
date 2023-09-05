# Python

## Profile function calls

```sh
python -m cProfile <script>
```

The results will be printed to standard output. Alternatively, supply
`-o <file>` to write directory to a file. Alternatively, pipe the terminal
standard output to a file.

Also, the function table can be sorted.
([See for details](https://docs.python.org/3/library/profile.html#pstats.Stats.sort_stats))
To sort by cumulative time, meaning total time of functions and their
sub-functions, run:

```sh
python -m cProfile -s cumtime <script>
```

## Enable truecolor support in IPython REPL

By default truecolor support is disabled in IPython. This can render highlight
colors (e.g. pop-up menus) unreadable when run from a terminal with the
truecolor setting enabled.

To enable truecolor support in IPython itself, generate an IPython config file
by running:

```sh
ipython profile create
```

This will create a directory in `${HOME}/.ipython`. Inside the directory, edit
the `ipython_config.py` file and change:

```python
c.TerminalInteractiveShell.true_color = True
```
