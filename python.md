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

## Import a file with non-standard file extension

To import a separate script that does not have a `.py` file extension, first
execute the following:

```python
from importlib.util import spec_from_loader, module_from_spec
from importlib.machinery import SourceFileLoader
import sys

spec = spec_from_loader("<modulename>", SourceFileLoader("<modulename>", "</path/to/input>"))
module = module_from_spec(spec)
spec.loader.exec_module(module)

sys.modules[<module_name>] = module
```

The code block will read the file and store it in `sys.modules` as a
locally-available module. Once done, use `import` or `from` to import from the
module as usual.

## Use a mutex

```python
import threading
import time
shared_counter = 0

# Mutex
mutex = threading.Lock()

# Function that will be executed by multiple threads
def increment_counter():
    global shared_counter
    # Acquire the mutex before modifying the shared counter
    mutex.acquire()
    try:
        # Critical section: access and modify the shared counter
        shared_counter += 1
        print(f"Thread {threading.current_thread().name} incremented counter to {shared_counter}")
    finally:
        # Release the mutex to allow other threads to acquire it
        mutex.release()

# Create multiple threads
threads = []
for i in range(3):
    thread = threading.Thread(target=increment_counter, name=f"Thread-{i}")
    threads.append(thread)

# Start the threads
for thread in threads:
    thread.start()

# Wait for all threads to finish
for thread in threads:
    thread.join()

print("Final value of shared counter:", shared_counter)
```
