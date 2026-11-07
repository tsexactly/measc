# measc

A small zsh script to measure the runtime of a line range in a C file.  
The measurement is inserted directly into the file and can be removed again afterwards.

## Setup

Clone the repository, navigate into it and execute:

```bash
./setup
```

This links the script into `/usr/local/bin`. Another directory can be passed as argument, e.g. `./setup ~/.local/bin`.

## Usage

```bash
measc -l 12 20 main.c
```

Inserts a time measurement around the lines 12 to 20 (inclusive). Compile and run the program as usual, the output looks like this:

```text
[measc] lines 12-20: 6.745 µs
```

```bash
measc -r main.c
```

Removes the measurement again. Every inserted line ends with `// measc`, so only these lines are removed.

## Notes

- The line range should contain complete statements (e.g. a whole loop including its closing bracket).
- If the range is executed multiple times (e.g. inside a loop), one line is printed per execution.
- With optimizations enabled (`-O2`), the compiler may remove calculations whose result is never used. The measurement then shows almost 0 µs.
- The clock is `CLOCK_MONOTONIC_RAW` (nanosecond resolution on macOS). On Linux, compile with `-std=gnu11` instead of `-std=c11` for it to be available.
