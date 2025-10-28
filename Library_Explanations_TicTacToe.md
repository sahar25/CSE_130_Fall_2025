# Explanation of Libraries Used in Tic-Tac-Toe Program

## `#include <iostream>`
- **Meaning:** "Input/Output Stream"  
- **Purpose:** Enables console input/output with:  
  - `std::cout` — print to screen  
  - `std::cin` — read from keyboard  
  - `std::endl` — new line  
- **C Equivalent:** `#include <stdio.h>`  
  (In C, you would use `printf()` and `scanf()` instead of `cout` and `cin`.)

---

## `#include <cstdlib>`
- **Meaning:** "C Standard Library"  
- **Purpose in this program:**  
  - `rand()` — generates random numbers  
  - `srand()` — seeds the random number generator  
- **Other functions (not used here):** `abs()`, `atoi()`, `malloc()`, etc.  
- **C Equivalent:** `#include <stdlib.h>`  
  (The same functions exist; `<cstdlib>` is the C++ version using the `std::` namespace.)

---

## `#include <ctime>`
- **Meaning:** "C Time Library" — provides time-related functions.  
- **Purpose in this program:**  
  - `time(0)` (or `time(NULL)`) returns the current time in seconds.  
  - Used as a seed for randomness: `srand(time(0));`  
- **C Equivalent:** `#include <time.h>`  
  (Same functions; `<ctime>` is the C++ version in the `std::` namespace.)

---

## `using namespace std;`
- **Purpose:** Allows using names like `cout`, `cin`, and `string` without writing `std::cout`, `std::cin`, etc.  
- It’s a convenience for short programs.  
- In larger or professional codebases, it’s better to avoid this in header files to prevent name conflicts.

---

## Summary Table

| C++ Library | Purpose | Example Functions/Objects | C Equivalent |
|--------------|----------|---------------------------|---------------|
| `<iostream>` | Input/output streams | `cout`, `cin`, `endl` | `<stdio.h>` |
| `<cstdlib>` | General utilities | `rand`, `srand`, `abs` | `<stdlib.h>` |
| `<ctime>` | Time/date utilities | `time`, `clock` | `<time.h>` |

---