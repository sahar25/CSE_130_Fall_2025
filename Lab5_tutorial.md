
# Lab Mini Tutorial — scanf, fgets, clearing buffer, rand/srand/time

## Function Signatures (memorize these)
```c
int scanf(const char *format, ...);
char *fgets(char *s, int n, FILE *stream);

int rand(void);
void srand(unsigned int seed);
time_t time(time_t *tloc);
```

## What each one does
- **`scanf`**: reads **formatted tokens** (e.g., `%d`, `%f`, `%s`). `%s` stops at whitespace. **Always bound** `%s` with a width: `"%31s"` for a 32‑byte buffer.
- **`fgets`**: reads **up to `n-1` chars** (including spaces) from a stream into `s`, **and adds a `'\0'`**. If there’s room and a newline is encountered, it **keeps the `'\n'`**. If the line is longer than the buffer, it **does not** include `'\n'`.
- **`rand`**: returns a pseudo‑random int in **[0, RAND_MAX]**.
- **`srand`**: **seeds** the PRNG. Call **once** at program start.
- **`time`**: returns **seconds since 1970‑01‑01 00:00:00 UTC** (Unix Epoch). Use it to seed `srand`.

---

## Safe `fgets` pattern (newline removal done **correctly**)
```c
#include <stdio.h>
#include <string.h>

char s[64];
if (fgets(s, sizeof(s), stdin)) {       // stdin = keyboard by default
    size_t n = strlen(s);
    if (n && s[n - 1] == '\n') {        // only strip if newline is present
        s[n - 1] = '\0';
    }
}
```
Why this check matters:
- If the input line **did not fit**, there may be **no `'\n'`** to remove.
- If the user just pressed **Enter on an empty line**, `strlen(s)` could be `1` and the last char is `'\n'` → safe to strip.
- Never do `s[strlen(s)-1]='\0'` **without** first checking `s[strlen(s)-1] == '\n'`.

---

## `scanf` + `fgets`: clear the buffer before switching
`scanf` often leaves the **newline** unread. Before calling `fgets` next, **discard** the rest of the current line:
```c
int c;
while ((c = getchar()) != '\n' && c != EOF) { }   // clear input buffer
```
> Do **not** use `fflush(stdin)` — undefined behavior.

Minimal token reads with bounds:
```c
char word[32];
scanf("%31s", word);   // read one space-delimited token safely
```

---

## Randomness: seed once, then use
```c
#include <stdlib.h>
#include <time.h>

srand((unsigned)time(NULL));   // in main()

int r = rand();                // 0..RAND_MAX
int coin = rand() % 2;         // 0 or 1
int idx  = rand() % count;     // random array index
```

---

## Tiny demo (all pieces together)
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>

int main(void) {
    srand((unsigned)time(NULL));

    char name[64], color[32];
    int age, c;

    // fgets: full line
    printf("Name: ");
    if (fgets(name, sizeof(name), stdin)) {
        size_t n = strlen(name);
        if (n && name[n-1]=='\n') name[n-1] = '\0';
    }

    // scanf: number, then clear buffer
    printf("Age: ");
    if (scanf("%d", &age) != 1) return 1;
    while ((c = getchar()) != '\n' && c != EOF) { }  // clear buffer

    // scanf: one word (bounded)
    printf("Favorite color (one word): ");
    if (scanf("%31s", color) != 1) return 1;

    const char *objects[] = {"laptop","bicycle","guitar"};
    int obj = rand() % 3;
    printf("\n%s is %d and likes a %s %s.\n", name, age, color, objects[obj]);
    return 0;
}
```
