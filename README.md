# Pipex

A 42 school project that replicates the behaviour of the shell pipe operator.
It takes two commands and connects them through a pipe, reading from an input
file and writing the final output to an output file — equivalent to running:

```
< infile cmd1 | cmd2 > outfile
```

## Author

ruortiz-

## What You Learn / Skills Acquired

- Unix process management: `fork`, `execve`, `waitpid`
- Inter-process communication (IPC) using pipes
- File descriptor manipulation with `dup2`, `open`, and `close`
- PATH resolution to locate executable commands at runtime
- Memory management in C (allocation, freeing, avoiding leaks)
- Build automation with Makefiles

## Build & Run

**Build:**

```bash
make
```

**Clean object files:**

```bash
make clean
```

**Full clean (objects + binary):**

```bash
make fclean
```

**Rebuild from scratch:**

```bash
make re
```

## Usage

```
./pipex infile cmd1 cmd2 outfile
```

| Argument  | Description                          |
|-----------|--------------------------------------|
| `infile`  | Path to the input file               |
| `cmd1`    | First command (reads from `infile`)  |
| `cmd2`    | Second command (reads from `cmd1`)   |
| `outfile` | Path to the output file              |

**Example** — count lines in `input.txt` that contain "hello":

```bash
./pipex input.txt "grep hello" "wc -l" output.txt
```

This is equivalent to:

```bash
< input.txt grep hello | wc -l > output.txt
```

## Project Structure

| File            | Description                                              |
|-----------------|----------------------------------------------------------|
| `pipex.c`       | Entry point: argument validation, pipe & fork management |
| `child.c`       | First and second child process logic                     |
| `utils.c`       | Command execution, PATH resolution, file helpers         |
| `check_error.c` | Exit-status inspection after child execution             |
| `pipex.h`       | Header: includes, macros, and function prototypes        |
| `libft/`        | Custom C library used throughout the project             |
| `Makefile`      | Build rules (`all`, `clean`, `fclean`, `re`)             |
