# iterm2-terminal

Some scripts that can help pwntools open iTerm2 from the container

## Why?

I don't like tmux when using pwntools to debug with GDB, so I made these scripts to use iTerm2 instead.

If you don't like tmux and prefer to use iTerm2, you come to the right place.

## Usage

1. When you `docker run` the container, add `-v /tmp/iterm2-terminal:/tmp/iterm2-terminal` to the options.

Something like this:

```bash
# original:
docker run -d --rm --name pwn-env --cap-add=SYS_PTRACE pwn-env
# add -v /tmp/iterm2-terminal:/tmp/iterm2-terminal :
docker run -d --rm --name pwn-env -v /tmp/iterm2-terminal:/tmp/iterm2-terminal --cap-add=SYS_PTRACE pwn-env
```

2. **In the container**, download [iterm2-terminal](./iterm2-terminal) into your `$PATH` and make it executable.

3. In your script that uses pwntools, use:

```python
from pwn import *
context.terminal = ['iterm2-terminal', '--option', '0']
...
```

Note:

- There are 4 options:
  - `--option 0`: Open GDB in a new pane, split vertically
  - `--option 1`: Open GDB in a new pane, split horizontally
  - `--option 2`: Open GDB in a new tab
  - `--option 3`: Open GDB in a new window

4. **In your macOS**, download [iterm2-terminal-docker](./iterm2-terminal-docker) into your `$PATH` and make it executable, then run it with the container name and the shell you want to use in your iTerm2:

e.g.

```bash
iterm2-terminal-docker --name=pwn-env --shell=zsh
```

5. In the same session of the shell you just opened, if you run the script with `gdb.debug()` or `gdb.attach()` in your container, it should open the GDB in iTerm2!

----

Feel free to open an issue if you have any questions or suggestions, also PRs are welcome!
