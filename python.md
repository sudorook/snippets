# Python

## Profile function calls

```sh
python -m cProfile <script>
```

The results will be printed to standard output. Alternatively, supply `-o
<file>` to write directory to a file. Alternatively, pipe the terminal standard
output to a file.

Also, the function table can be sorted. ([See for
details](https://docs.python.org/3/library/profile.html#pstats.Stats.sort_stats))
To sort by cumulative time, meaning total time of functions and their
sub-functions, run:
```
python -m cProfile -s cumtime <script>
```
