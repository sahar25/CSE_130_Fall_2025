
# 🎤 Lab #3 Tutorial

**Welcome!**  
Welcome to the **second best calculator in the world**—the best one is for the next lab 😉.  
To start your lab today, you’ll need to know these C concepts:

---

### 🖨️ 1. Input & Output
- `printf` → to talk to the user.  
- `scanf` → to listen to the user.  
(*We covered this in the last labs, so it should be second nature by now.*)

---

### 🔢 2. Integers vs Floats
- **Integers (`int`)**: whole numbers like 5, -2, 42.  
- **Floats (`float`/`double`)**: numbers with decimals like 3.14, 2.71.  
⚠️ Watch out: division with integers chops off the decimals (e.g., `7/2 = 3`, not 3.5).

---

### 🔁 3. Loops
We’ll use a **do-while loop** to keep showing the calculator menu until the user chooses Exit.

```c
int choice;
do {
    printf("Enter a number (0 to quit): ");
    scanf("%d", &choice);
    printf("You typed %d\n", choice);
} while (choice != 0);
```
---

### ⚖️ 4. Conditions
Two tools:  
- **if/else** → for decisions.  
- **switch** → for menu selection.  

**Example inside the do-while:**
```c
int choice;
do {
    printf("Enter a number (0 to quit): ");
    scanf("%d", &choice);
    printf("You typed %d\n", choice);
} while (choice != 0);
```
---
### 🔎 5. Prime Numbers
- **A prime number** is a natural number greater than 1 that has no divisors other than 1 and itself.  
- Examples: 2, 3, 5, 7, 11… 
- Non-prime example: 22, because 2 × 11 = 22.
---
### 🎉Let's wrap up
So technically this is just C code, but since it’s interactive and actually useful, let’s proudly call it your first little app.

---


