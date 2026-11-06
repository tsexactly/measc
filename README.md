# measurec

Two small zsh scripts to measure the runtime of a line range in a C file.
`measurec` inserts the measurement directly into the file, `unmeasurec` removes it again.

## Setup

Clone the repository, navigate into it and execute:

```bash
./setup
```

This links both scripts into `/usr/local/bin`. Another directory can be passed as argument, e.g. `./setup ~/.local/bin`.

## Usage

```bash
measurec main.c 12 20
```

Inserts a time measurement around the lines 12 to 20 (inclusive). Compile and run the program as usual, the output looks like this:

```text
[measurec] lines 12-20: 6.745 us
```

```bash
unmeasurec main.c
```

Removes the measurement again. Every inserted line ends with `// measurec`, so only this lines are removed.

## Notes

- The line range should contain complete statements (e.g. a whole loop including its closing bracket).
- If the range is executed multiple times (e.g. inside a loop), one line is printed per execution.
- With optimizations enabled (`-O2`), the compiler may remove calculations whose result is never used. The measurement than shows almost 0 us.
- The clock is `CLOCK_MONOTONIC_RAW` (nanosecond resolution on macOS). On Linux, compile with `-std=gnu11` instead of `-std=c11` for it to be available.
