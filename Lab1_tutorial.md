# CSE 130 Lab 1 Tutorial: ASCII Art in C

## Deadline: August, 29

Welcome to your first lab for CSE 130! This is going to be a fun and engaging experience. For some of you, this might be your first programming assignment—exciting, right? 

Today, we’ll focus on combining creativity with coding by creating an **ASCII art representation** of Dr. Yampolskiy, your instructor. It doesn’t have to be a masterpiece, but it should clearly depict him teaching CSE 130. Let’s dive in!

---

## What Will You Be Doing in This Lab?

You’ll be writing a **C program** that generates an original ASCII art picture of Dr. Yampolskiy. But first, let’s clarify a few basics:

1. **What is coding?**
   - Coding is the process of converting an **algorithm** into a working program.
   - There are various programming languages, and we’ll start with **C**, a high-level programming language.

2. **What is source code?**
   - The text you write in C is called **source code**.
   - You save this code in a file with a `.c` extension.

---

## Tools You’ll Need

Before we can write any code, let’s ensure you have the necessary tools:

1. **Install an IDE (Integrated Development Environment):**
   - For this lab, we’ll use **Bloodshed Dev-C++**, as specified on the course Blackboard.
   - Note: Bloodshed requires **Windows OS**. Make sure you’ve installed it before proceeding.
You can download it from  the following link (https://sourceforge.net/projects/embarcadero-devcpp/)
2. **Setting up your IDE:**
   - Once installed, your IDE should look like this:
     ![image](https://github.com/user-attachments/assets/a3738dbc-d18c-4e9e-bc89-4828a26a5491)

   - You’ll use it to create, compile, and run your first C program.

---

## Writing Your First C Program

Here’s what you need to know to get started:

1. **Creating a New File:**
   - Open Bloodshed and create a new file.
   - Save it with a `.c` extension (e.g., `lab1.c`).

2. **Structure of a C Program:**
   - Every C program includes **headers**, like `#include <stdio.h>`. For today’s lab, we’ll focus on `stdio.h` for input/output operations.
   - The program starts with a `main()` function. The compiler looks for this function to execute the program.

3. **Printing to the Console:**
   - Use `printf()` to display text. For example:
     ```c
     printf("Hello, World!\n");
     ```
   - Text inside `printf()` should be enclosed in double quotes (`""`).

4. **Using Escape Sequences:**
   - **Escape sequences** are special characters that let you format your output. Examples include:
     - `\n` for a new line.
     - `\t` for a tab space.
   - These are essential for designing your ASCII art layout.

---

## Tips for Your ASCII Art Program

- **Be Creative**: Your code should be original and well-commented.
- **Commenting**: Include details like:
  - Author’s name
  - Lab section
  - Date
  - A brief program description
- **Bug-Free Code**: Test your program thoroughly to ensure it works as expected.

Here’s a quick example to inspire you:

```c
#include <stdio.h>

int main() {
    printf("  ****\n");
    printf(" *    *\n");
    printf("* Dr. Y *\n");
    printf(" *    *\n");
    printf("  ****\n");
    return 0;
}
```

This is just a basic structure. Your final output should resemble Dr. Yampolskiy teaching.

---

## Good Luck!

Good luck with your first lab! Remember, this is a chance to learn, have fun, and get creative with programming. Let’s make Dr. Yampolskiy proud!

