# ☎️ Lab 7 Tutorial — Advanced Phone Book (C)

In this lab, you will **extend your Lab 6 dynamic phone book** by adding new and more powerful features.  
You’ll continue practicing dynamic memory management, modular functions, and string manipulation — now with **searching, sorting, and random selection**.

---

## 0) Concepts from previous labs you’ll reuse
- **Dynamic arrays** with `malloc`, `realloc`, `free`
- **Structures** to store contacts
- **Menu loops** using `do { … } while`
- **String handling** (`fgets`, removing `\n`, etc.)
- **Random numbers** with `rand`, `srand`, and `time`

---

## 1) New features required in Lab 7
Add these functionalities to your previous Lab 6 phonebook program:

### 1️⃣ Sort entries alphabetically by name
- Ask the user whether to sort by **first name** or **last name**.
- Use a **sorting algorithm** such as **Bubble Sort** or **Selection Sort**.
- Use **case-insensitive string comparison** to ensure `"Alice"` and `"alice"` are treated as the same order alphabetically.

### 2️⃣ Find a phone number for a given name
- Prompt for a name (first and last).
- Compare using a **case-insensitive comparison** (`strcasecmp`) and print the result if found.

### 3️⃣ Randomly select a friend to call
- Generate a random index using:
  ```c
  srand(time(NULL));
  int index = rand() % pb->size;
```
- Print the selected contact’s name and number.

### 4️⃣ Delete everyone from the phonebook
Loop through all entries and free() any dynamically allocated strings.

Reset the size to zero and optionally shrink memory with realloc(pb->data, 0); works also.

## 2) Case-Insensitive String Comparison
By default, strcmp() is **case-sensitive**, so "Alice" and "alice" would not be treated as equal.
To compare strings alphabetically ignoring case, use **strcasecmp()** from <strings.h>:
 ```c
#include <strings.h>  // for strcasecmp
 ```
Usage
 ```c
if (strcasecmp(a, b) > 0) {
    // a comes after b alphabetically
}
 ```
If your compiler doesn’t support it, you can write a custom version using tolower() from <ctype.h>.
## 3) Sorting Function Example (Bubble Sort)
Here’s an example sort_contacts() function using Bubble Sort and strcasecmp():
 ```c
#include <strings.h>  // for strcasecmp
#include <ctype.h>    // for tolower

void sort_contacts(PhoneBook *pb, int by_first) {
    for (int i = 0; i < pb->size; i++) {
        for (int j = 0; j < pb->size - i - 1; j++) {
            const char *a = by_first ? pb->data[j].first : pb->data[j].last;
            const char *b = by_first ? pb->data[j + 1].first : pb->data[j + 1].last;
            if (strcasecmp(a, b) > 0) {
                Contact temp = pb->data[j];
                pb->data[j] = pb->data[j + 1];
                pb->data[j + 1] = temp;
            }
        }
    }
    puts("Contacts sorted alphabetically (case-insensitive).");
}
 ```
## 4) Function suggestions
Expand your Lab 6 file with new helper functions:
 ```c
void sort_contacts(PhoneBook *pb, int by_first);
void find_contact(const PhoneBook *pb);
void random_contact(const PhoneBook *pb);
void clear_phonebook(PhoneBook *pb);
 ```
Each should perform exactly one task and be called from the menu.
## 5) Updated Menu Example
 ```c

do {
    puts("Phone Book Application — Lab 7");
    puts(" 1) Add friend");
    puts(" 2) Delete friend");
    puts(" 3) Show phone book");
    puts(" 4) Sort contacts");
    puts(" 5) Find phone number");
    puts(" 6) Random friend to call");
    puts(" 7) Delete everyone");
    puts(" 0) Exit");
    printf("Choice: ");
    scanf("%d", &choice);
    int ch; while ((ch = getchar()) != '\n' && ch != EOF) {}

    switch (choice) {
    case 1: add_contact(&pb); break;
    case 2: delete_contact(&pb); break;
    case 3: show_phonebook(&pb); break;
    case 4: sort_contacts(&pb, 1); break;  // or ask user which field
    case 5: find_contact(&pb); break;
    case 6: random_contact(&pb); break;
    case 7: clear_phonebook(&pb); break;
    case 0: break;
    default: puts("Invalid choice.");
    }
} while (choice != 0);

 ```
---
## 6) Tips & Pitfalls

- Always call srand(time(NULL)) once at the start of main().
- When sorting, swap entire structs, not just one field.
- For search, convert both sides to the same case or use strcasecmp.
- Check that the phonebook is not empty before sorting or selecting randomly.
- Always free all memory before exiting or clearing.
---

## 7) Minimal Requirements Recap

✅ Works with your Lab 6 phonebook (same structs and memory logic)
✅ Adds menu options for sort, find, random, and delete-all
✅ Uses case-insensitive string comparison (strcasecmp)
✅ Implements and calls a sorting function (like Bubble Sort)
✅ Frees all memory and handles edge cases

---
ALL THE BEST :) !!
