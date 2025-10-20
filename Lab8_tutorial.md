# 🗂️ Lab 8 — Phonebook Save & Load (C)

This lab adds **file saving and loading** to your Lab 7 dynamic phonebook.  
You’ll make it possible to **store contacts to a file** and **read them back** later.

---

## 🧩 Goal
Make your phonebook able to:
1. **Save** all contacts into a file path specified by the user.  
2. **Load** contacts from that file when the program starts again.  
3. Use a **default file name** (e.g., `contacts.txt`) if the user presses *Enter* without typing a path.

---

## 🗃️ File Format
Each contact is stored in one line, with fields separated by tabs:

```
first    last    phone
```

Example:
```
Ada    Lovelace    +1 502 123 4567
```

---

## 🧠 Needed Functions
You’ll use:
- `fopen(path, mode)` → open file (`"w"` to write, `"r"` to read)`  
- `fprintf()` → write formatted text  
- `fgets()` → read one line  
- `fclose()` → close file  

---

## 💾 Save Function

```c
int save_to_file(PhoneBook *pb, const char *path) {
    const char *filename = (path && *path) ? path : "contacts.txt";
    FILE *f = fopen(filename, "w");
    if (!f) {
        printf("Error: could not open %s for writing.\n", filename);
        return 0;
    }

    for (int i = 0; i < pb->size; i++) {
        fprintf(f, "%s\t%s\t%s\n",
                pb->data[i].first,
                pb->data[i].last,
                pb->data[i].phone);
    }

    fclose(f);
    return 1;
}
```

---

## 📂 Load Function

```c
int load_from_file(PhoneBook *pb, const char *path) {
    const char *filename = (path && *path) ? path : "contacts.txt";
    FILE *f = fopen(filename, "r");
    if (!f) {
        printf("Error: could not open %s for reading.\n", filename);
        return 0;
    }

    // TO DO
    pb->size = 0; // start fresh
    // make sure to delete all contacts before you start loading the file

    char first[50], last[50], phone[50];

    while (fscanf(f, "%s\t%s\t%s", first, last, phone) == 3) {
        // add_contact should dynamically allocate memory (like in Lab 7)
        add_contact(pb, first, last, phone);
    }

    fclose(f);
    return 1;
}
```

---

## 🧭 Menu Update

Add two new options:
```
8) Save to file
9) Load from file
```

Example:

```c
case 8:
    printf("Enter path (Enter for default): ");
    // TO DO always clear buffer when needed
    fgets(path, sizeof path, stdin);
    if (save_to_file(&book, path)) printf("Saved!\n");
    else printf("Save failed!\n");
    break;

case 9:
    printf("Enter path (Enter for default): ");
    // TO DO always clear buffer when needed
    fgets(path, sizeof path, stdin);
    if (load_from_file(&book, path)) printf("Loaded!\n");
    else printf("Load failed!\n");
    break;
```

---

## 🧾 Updated Menu Example

```c
do {
    puts("Phone Book Application — Lab 8");
    puts(" 1) Add friend");
    puts(" 2) Delete friend");
    puts(" 3) Show phone book");
    puts(" 4) Sort contacts");
    puts(" 5) Find phone number");
    puts(" 6) Random friend to call");
    puts(" 7) Delete everyone");
    puts(" 8) Save to file");
    puts(" 9) Load from file");
    puts(" 0) Exit");
    printf("Choice: ");

    scanf("%d", &choice);
    int ch; while ((ch = getchar()) != '\n' && ch != EOF) {}

    switch (choice) {
        case 1: add_contact(&pb); break;
        case 2: delete_contact(&pb); break;
        case 3: show_phonebook(&pb); break;
        case 4: sort_contacts(&pb, 1); break;  // you may ask user: sort by first or last name
        case 5: find_contact(&pb); break;
        case 6: random_contact(&pb); break;
        case 7: clear_phonebook(&pb); break;
        case 8:...; break;
        case 9: ...; break;
        case 0: break;
        default: puts("Invalid choice.");
    }
} while (choice != 0);
```

---

## ✅ Test Checklist
- Add a few contacts → Save → Exit → Run again → Load → See same contacts.  
- Press Enter to use default `contacts.txt`.  
- Try invalid paths → should print “Save failed” or “Load failed.”  

---

## 💡 Tips
- Always **close files** (`fclose`) when done.  
- Don’t forget to **clear the input buffer** after using `scanf`.  
- Keep your Lab 7 features working: Add / Delete / Show / Sort, etc.  
