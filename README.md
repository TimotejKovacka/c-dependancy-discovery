# c-dependancy-discovery

## Overview

`dependencyDiscoverer` is a tool designed to analyze C, Yacc, and Lex source files to determine file dependencies for use in makefiles. It processes specified source files to generate a list of dependencies between object files (.o), source files (.c, .l, .y), and included header files (.h).

## Features

- Processes `.c`, `.l`, and `.y` files to generate a make-compatible dependency list.
- Handles both local (`#include "file.h"`) and specified directories for headers with `-I`.
- Supports `CPATH` environment variable to specify additional include directories.
- Outputs dependencies directly to standard output for easy integration with build systems.
- Threaded processing for efficient handling of multiple files.

## Usage

```bash
./dependencyDiscoverer [-Idir]... file.c|file.l|file.y...
```

### Options

- `-Idir`: Specify additional directories to search for included header files. Directories are searched in the order they are specified before falling back to the standard include paths defined in `CPATH`.

### Arguments

- `file.c|file.l|file.y`: Source files to be processed. The tool supports C files (.c), Lex files (.l), and Yacc files (.y).

## Examples

Generate dependencies for a single C file:

```bash
./dependencyDiscoverer example.c
```

Generate dependencies for multiple C files with additional include directories:

```bash
./dependencyDiscoverer -I./include -I/usr/local/include file1.c file2.c
```

Using environment variable CPATH to specify include paths:

```bash
export CPATH="/home/user/include:/usr/local/include"
./dependencyDiscoverer file.c
```

## Testing

The program can be tested against `test` directory with the following command:

```bash
./dependencyDiscoverer -I./test ./test/*.c
```

## Installation

1. Clone the Repository:

```bash
git clone https://github.com/TimotejKovacka/c-dependancy-discovery
```

2. Compile the Program:

```bash
g++ -o dependencyDiscoverer dependencyDiscoverer.cpp -std=c++11 -lpthread
```

3. Set the CPATH Environment Variable (Optional):
   Add desired include paths to your shell configuration

```bash
export CPATH="/path/to/includes"
```

## System Requirements

- GCC Compiler with C++11 support.
- Linux or Unix-like operating system.

## License

This project is licensed under the [MIT License](./LICENSE).
