*This project has been created as part of the 42 curriculum by hsennane.*

# Libft

## Description

**Libft** is a foundational C project from the **42 / 1337 curriculum**. The objective is to recreate useful functions from the C standard library and build additional helpers for future programming projects.

It provides practice with **pointers**, **strings**, **memory allocation**, **arrays**, **character handling**, and **static library compilation**.

The current Makefile builds **34 functions** into `libft.a`. This repository contains the main utility functions; **bonus linked-list functions are not included**.

## Instructions

### Building the Project

You need `make`, a C compiler, and the standard Unix build tools.

```bash
git clone https://github.com/hajarsen/final_libft.git
cd final_libft
make
```

The build creates **`libft.a`** with the compiler flags `-Wall -Wextra -Werror`.

### Using the Library

Create `main.c` in the repository:

```c
#include "libft.h"
#include <stdio.h>

int main(void)
{
    printf("Length: %zu\n", ft_strlen("Libft"));
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

### Makefile Commands

| Command | Action |
|---|---|
| `make` / `make all` | Build `libft.a` |
| `make clean` | Remove `.o` files |
| `make fclean` | Remove objects and the library |
| `make re` | Recompile everything |

### Functions Included

| Category | Functions |
|---|---|
| Character checks | `ft_isalpha`, `ft_isdigit`, `ft_isalnum`, `ft_isascii`, `ft_isprint` |
| Character conversion | `ft_toupper`, `ft_tolower` |
| String operations | `ft_strlen`, `ft_strchr`, `ft_strrchr`, `ft_strncmp`, `ft_strnstr`, `ft_strlcpy`, `ft_strlcat`, `ft_strdup` |
| Memory operations | `ft_memset`, `ft_bzero`, `ft_memcpy`, `ft_memmove`, `ft_memchr`, `ft_memcmp`, `ft_calloc` |
| Number conversion | `ft_atoi`, `ft_itoa` |
| String helpers | `ft_substr`, `ft_strjoin`, `ft_strtrim`, `ft_split`, `ft_strmapi`, `ft_striteri` |
| Output functions | `ft_putchar_fd`, `ft_putstr_fd`, `ft_putendl_fd`, `ft_putnbr_fd` |

### Project Structure

```text
final_libft/
├── libft.h        # Function declarations
├── ft_*.c         # One source file per function
├── Makefile       # Builds the static library
└── README.md
```

### Evaluation Notes

- Understand each function's expected behavior, especially at boundaries.
- Always check memory allocation results when writing new code.
- Functions that return allocated memory need the caller to release it when appropriate.
- No automated testing suite is included in this repository.
- There are no bonus linked-list functions in the current build.

## Resources

Below are concise explanations of the most important concepts used throughout Libft.

---

## 🧠 Pointers and Memory

A **pointer** stores the address of another object in memory.

```text
int number = 42;
int *ptr = &number;

     variable             memory (illustrative)
   ┌────────────┐         ┌───────────────────┐
   │ ptr        │────────►│ number = 42       │
   │ address    │         │ address: 0x1000   │
   └────────────┘         └───────────────────┘

*ptr  → value at the address stored in ptr
&number → address of number
```

### Stack vs Heap (Simplified)

```text
        PROGRAM MEMORY
  ┌─────────────────────────┐
  │ Stack                   │
  │ Local variables         │
  │ Function call state     │
  ├─────────────────────────┤
  │ Heap                    │
  │ Dynamically allocated   │
  │ memory (malloc/calloc)  │
  └─────────────────────────┘

malloc / calloc → allocate memory
free            → release allocated memory
```

In this project, functions such as `ft_strdup`, `ft_substr`, `ft_strjoin`, `ft_split`, `ft_itoa`, and `ft_calloc` can return dynamically allocated memory.

---

## 🔤 C Strings

A C string is a sequence of characters ending with the **null terminator** `'\0'`.

```text
String: "42"

Index:      0       1       2
         ┌───────┬───────┬────────┐
Value:   │  '4'  │  '2'  │  '\0'  │
         └───────┴───────┴────────┘

ft_strlen("42") = 2
Storage needed  = 3 bytes
```

### Useful String Functions

- `ft_strlen` measures the number of characters before `'\0'`.
- `ft_strchr` searches for the **first** occurrence of a character.
- `ft_strrchr` searches for the **last** occurrence.
- `ft_substr` produces a new substring.
- `ft_strjoin` produces a new string by concatenating two strings.
- `ft_split` divides a string into an array of strings using a delimiter.

### How Splitting Works

```text
Input: "red,green,blue"
Delimiter: ','

           ft_split
               │
               ▼
       ┌─────────────┐
       │   "red"     │
       │   "green"   │
       │   "blue"    │
       │   NULL      │
       └─────────────┘
```

The returned array and its allocated strings must eventually be freed by the caller.

---

## 🔁 Memory Operations

Memory functions work on a **number of bytes**, unlike many string functions that stop at `'\0'`.

### memcpy vs memmove

`memcpy` copies a block of bytes but requires that source and destination **do not overlap**. `memmove` is designed to handle overlapping regions correctly.

```text
Original bytes:
┌───┬───┬───┬───┬───┐
│ A │ B │ C │ D │ E │
└───┴───┴───┴───┘
  └─────────┐
  Copy 3 bytes one position right
            ▼
Expected result using memmove:
┌───┬───┬───┬───┬───┐
│ A │ A │ B │ C │ E │
└───┴───┴───┴───┘
```

| Function | Main purpose |
|---|---|
| `ft_memset` | Fill bytes with a value |
| `ft_bzero` | Set bytes to zero |
| `ft_memcpy` | Copy non-overlapping memory |
| `ft_memmove` | Copy memory safely when regions overlap |
| `ft_memchr` | Find a byte in memory |
| `ft_memcmp` | Compare blocks of memory |
| `ft_calloc` | Allocate zero-initialized memory |

---

## 🧮 String and Number Conversion

### ft_atoi

`ft_atoi` interprets the beginning of a string as a decimal integer.

```text
Input: "  -123abc"
         │
         ├─ Skip leading whitespace
         ├─ Read '-' sign
         ├─ Parse '1', '2', '3'
         └─ Stop at 'a'

Result: -123
```

### ft_itoa

`ft_itoa` performs the reverse kind of conversion by creating a newly allocated string representing an integer.

```text
Integer: -42
    │
    ▼
ft_itoa(-42)
    │
    ▼
String: "-42"
```

---

## 🛠️ Static Library Compilation

A **static library** collects compiled object files into a reusable archive.

```text
ft_strlen.c ──► ft_strlen.o ──┐
ft_atoi.c ────► ft_atoi.o ───┤
other ft_*.c ─► other .o ────┤
                             ▼
                          libft.a
                             │
                       linked with
                             │
                           main.c
                             ▼
                         executable
```

This is useful in later 42 projects: include `libft.h` and link the archive during compilation.

---

## 🎯 Libft Tips

1. Test empty strings, null pointers where supported, and boundary conditions.
2. Distinguish byte operations from null-terminated string operations.
3. Verify allocations and free memory when it is no longer needed.
4. Pay attention to integer limits and buffer sizes.
5. Compile with the project's warning flags after every change.

### Useful Links

- [C language reference — cppreference](https://en.cppreference.com/w/c)
- [malloc and free — cppreference](https://en.cppreference.com/w/c/memory/malloc)
- [GNU Make manual](https://www.gnu.org/software/make/manual/)

### AI Usage

AI assistance was used to **organize this README, explain underlying C concepts, and prepare educational diagrams**. The documentation update does not change the C source code.
