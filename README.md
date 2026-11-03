# Libft

My implementation of a small C utility library for the **42 / 1337 curriculum**.

The aim of this project is to recreate common C library functions and learn how to work with pointers, memory allocation, strings, linked concepts, and static libraries.

## Features

The project includes **34 functions** grouped into a few categories.

| Category | Functions |
| --- | --- |
| Character checks | `ft_isalpha`, `ft_isdigit`, `ft_isalnum`, `ft_isascii`, `ft_isprint` |
| Character conversion | `ft_toupper`, `ft_tolower` |
| Strings | `ft_strlen`, `ft_strchr`, `ft_strrchr`, `ft_strncmp`, `ft_strnstr`, `ft_strlcpy`, `ft_strlcat`, `ft_strdup` |
| Memory | `ft_memset`, `ft_bzero`, `ft_memcpy`, `ft_memmove`, `ft_memchr`, `ft_memcmp`, `ft_calloc` |
| Conversion | `ft_atoi`, `ft_itoa` |
| String helpers | `ft_substr`, `ft_strjoin`, `ft_strtrim`, `ft_split`, `ft_strmapi`, `ft_striteri` |
| File-descriptor output | `ft_putchar_fd`, `ft_putstr_fd`, `ft_putendl_fd`, `ft_putnbr_fd` |

## Installation

Clone the repository and build the static library:

```bash
git clone https://github.com/hajarsen/final_libft.git
cd final_libft
make
```

This creates `libft.a`, which you can link with other C programs.

**Requirements:** a C compiler and `make`. The Makefile uses `cc`, `ar`, and the flags `-Wall -Wextra -Werror`.

## Usage example

Create a file named `main.c` in the repository:

```c
#include "libft.h"
#include <stdio.h>

int main(void)
{
    char *name = "Libft";

    printf("Length: %zu\n", ft_strlen(name));
    printf("Uppercase: %c\n", ft_toupper('a'));
    printf("Number: %d\n", ft_atoi("42"));
    ft_putendl_fd("Hello from Libft!", 1);
    return (0);
}
```

Compile and run:

```bash
cc -Wall -Wextra -Werror main.c libft.a -o demo
./demo
```

Expected output:

```text
Length: 5
Uppercase: A
Number: 42
Hello from Libft!
```

## Makefile commands

| Command | Description |
| --- | --- |
| `make` | Compile the library |
| `make all` | Compile the library |
| `make clean` | Remove object files |
| `make fclean` | Remove object files and `libft.a` |
| `make re` | Rebuild the library |

## Project structure

```text
final_libft/
├── Makefile
├── libft.h
├── ft_*.c
└── README.md
```

Each function is implemented in a separate C source file, with declarations in `libft.h`. The Makefile compiles the source files and archives the object files into `libft.a`.

## What I practiced

- Pointers and memory management
- Manipulating C strings and arrays
- Allocating and freeing memory
- Working with file descriptors
- Building and linking a static library
- Writing reusable C functions

## Notes

This repository contains the functions listed in its Makefile. It does **not** declare or build the bonus linked-list functions. The README describes the current project contents; it is not a claim of automated test coverage.

## Author

**hsennane** — 42 / 1337 project.
