# 🗃️ Lab 6 Tutorial — Dynamic Phone Book (C)

This lab asks you to build a **phone book** that stores contacts in a **dynamic array of structs**, with options to **add**, **delete**, and **show** entries. Names are unique. You must allocate and free memory as needed and avoid printing invalid/`NULL` entries.

---

## 0) Concepts from previous labs you’ll use
- **Loops**: `do { … } while (condition);`, `for`
- **Menus & input validation**
- **`sizeof`** for types and objects
- **Strings**: creating buffers, reading with `scanf` / `fgets`, writing with `printf`
- **Basic functions**: prototypes, separate helpers for each menu action

---

## 1) New concepts for this lab
### A. `struct` — grouping related fields
Use a structure to keep a contact’s fields together:
```c
typedef struct {
    char *first;
    char *last;
    char *phone;
} Contact;
```

### B. Where to keep the **dynamic array**
The lab only requires that you allocate and free memory as needed. Both strategies are valid:
- **Exact-fit strategy**: `realloc` array size to exactly `size` after every insert/delete.
- **Amortized growth strategy**: keep a `capacity` field and grow (e.g., double) when needed.

You can organize this in two ways:

**Option 1 — Wrap in a `PhoneBook` struct:**
```c
typedef struct {
    Contact *data;     // heap array of Contact
    size_t   size;     // number of used slots
    size_t   capacity; // allocated slots
} PhoneBook;
```

**Option 2 — Track raw dynamic array + counters:**
```c
Contact *contacts;  // heap array
size_t   size; ( optional)
size_t   capacity; ( optional)
```

Both designs satisfy the lab requirements.

### C. Dynamic memory: `malloc`, `calloc`, `realloc`, `free`
- `malloc(bytes)` → uninitialized memory.
- `calloc(n, size)` → zero-initialized.
- `realloc(ptr, new_bytes)` → resize, may move memory.
- `free(ptr)` → release.

### D. String comparison: `strcmp`
- `strcmp(a, b)` → case-sensitive, returns 0 if equal.

Use this to check for unique names and to delete by name.

---

## 2) Headers to include
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>   // for strcmp, strlen, etc.
```

---

## 3) Function **signatures** (no implementations here)
If you use the **PhoneBook struct**:
```c
// lifecycle
void pb_init(PhoneBook *pb);
void pb_free(PhoneBook *pb);

// helpers ( optional)
int  pb_find_index(const PhoneBook *pb, const char *first, const char *last);
void pb_ensure_capacity(PhoneBook *pb, size_t min_capacity);

// required actions
void add_contact(PhoneBook *pb);
void delete_contact(PhoneBook *pb);
void show_phonebook(const PhoneBook *pb);
```

If you use the **raw array approach**, mirror the signatures with `Contact **contacts (, size_t *size, size_t *capacity`).

---

## 4) Menu loop (only showing calls)
```c
int main(void) {
    PhoneBook pb;
    int choice;

    pb_init(&pb);

    do {
        puts("Phone Book Application");
        puts(" 1) Add friend");
        puts(" 2) Delete friend");
        puts(" 3) Show phone book");
        puts(" 0) Exit");
        printf("What do you want to do: ");
        scanf("%d", &choice);
        int ch; while ((ch = getchar()) != '\n' && ch != EOF) {}

        switch (choice) {
        case 1: add_contact(&pb); break;
        case 2: delete_contact(&pb); break;
        case 3: show_phonebook(&pb); break;
        case 0: break;
        default: puts("Invalid choice.");
        }
        puts("");
    } while (choice != 0);

    pb_free(&pb);
    return 0;
}
```

## 5) Tips & pitfalls
- Always check results of `malloc`/`realloc`.
- With `realloc`, assign to a temporary pointer.
- Every allocation must be freed.
- Strip `\n` after `fgets`.
- Use `strcmp`, not `==`, to compare strings.
- Maintain consistent `size` and `capacity`.

---

## 6) Minimal requirements recap
- A `struct` for contacts.
- A **dynamic array** on the heap (with or without wrapper struct).
- Uses `malloc`/`calloc`/`realloc`/`free` correctly.
- Uses `strcmp` for name checks (unique names).
- Menu with add/delete/show.
- No invalid/NULL entries printed.
- Frees all memory on exit.
