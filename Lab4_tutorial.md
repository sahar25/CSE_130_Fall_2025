
# 🧮 Lab #4 Tutorial — “Second Best Calculator 2.0”

**Welcome back!**  
Today you’ll be using **functions**, plus add **factorial**, **power**, and a **sequence generator** that stores results in an **array** and prints a sequence.

---

## 🧱 0) What carries over from Lab 3
Your calculator should still support:
- Addition, subtraction, multiplication, division
- Modulus, Prime test (integers only)
- Menu loop with “Exit” option

---

## 🧩 1) New concepts for Lab 4 (what & why)
- **Functions** → Each menu action becomes its own function (cleaner, reusable, easier to test).
- **Factorial** → `n!` multiplies all integers from 1 to `n`. By definition **`0! = 1`**.
- **Power** → Raise a **float** base to an **integer** exponent.
- **Arrays + sequences** → Compute the first *n* terms of a sequence (e.g., **Fibonacci**, **Prime Numbers**) and store them in an array before printing.

> We’ll define these briefly now; you’ll implement them “for real” in the code section below.

---

## 🧠 2) Function anatomy (review)
**Prototype → Definition → Call**
```c
// Prototype (top of file)
int add(int a, int b);

// Definition
int add(int a, int b) { return a + b; }

// Call
int s = add(3, 4);
```
**Why functions?**
-   Clear responsibilities, fewer bugs, easier grading, easier to extend later.
----------

## ✳️ Factorial — definition & rules

-   **Definition:**  
    For an integer `n ≥ 0`,  
    `n! = 1 × 2 × 3 × … × n` and **`0! = 1`**.
    
-   **Domain:** integers only; negative `n` is **not defined** for this lab.
    
-   **Overflow note:** even 64-bit integers overflow quickly, you might want to use **long**
    

**Example function signature:**

```c
// Returns: factorial in unsigned long long; sets *ok=0 on error (e.g., n<0 or overflow)  
unsigned  long  long  factorial(int n, int *ok);
```

----------

## ️⚡ Power — definition & rules

-   **Definition (for this lab):** raise a **float base** to an **integer exponent**.
    
-   **Signature choice:**
    
    -   Base: `double` or `float` (handles decimals)
        
    -   Exponent: `int` (whole number)
        
-   **Exceptions / edge cases to mention:**
    
    -   **Negative exponents**: allowed if you want—return `1 / (base^|exp|)` (but reject if base is `0`).
        
    -   **Zero cases:**
        
        -   `base^0 = 1` (even if `base` is 0)
            
        -   `0^positive = 0`
            
        -   `0^negative` is **undefined** → print an error
            
-   **Advanced Implementation tip:** use **fast exponentiation** for integer exponents.
    

**Example function signature:**

```c
// Returns base^exp, where base is double, exp is int (can be >=0; support <0 if you want) 
double  dpow(double base, int  exp, int *ok);
```
----------

## 🌀 Fibonacci — definition & rules

-   **Definition:**  
    `F0 = 0`, `F1 = 1`, and for `n ≥ 2`: `Fn = F(n-1) + F(n-2)`.
    
-   **Goal:** ask the user for `n`, compute the first `n` terms, store them in an array, then print them.
    
-   **Edge cases:**
    
    -   `n = 1` → print `0`
        
    -   `n = 2` → print `0 1`
        
## 🧩 3) Putting it together (menu sketch)

> You will route menu choices to functions. This is just a sketch—fill in prompts & checks as you did in Lab 3.

```c
int choice; 
do {
  printf("\nMenu:\n");
  printf("(1) Add  (2) Sub  (3) Mul  (4) Div  (5) Mod\n");
  printf("(6) Prime  (7) Factorial  (8) Power  (9) Fibonacci  (0) Exit\n");
  // read `choice` safely (check scanf return)  
  // ...  
  switch (choice) { 
    case  7: /* factorial */  break;
    case  8: /* power */  break; 
    case  9: /* fibonacci */  break; 
    // others from Lab 3...  
    case  0: printf("Good Bye!"); break; 
    default: printf("Unknown choice.");
  }
} while (choice != 0);
```
## 🧪 5) Quick test ideas

-   Factorial: `0!` (should be 1), `1!`, `5!`, `20!`, and try `21!` → should error/overflow.
    
-   Power: `2^0`, `2^10`, `(-2)^3`, `0^5`, `0^-1` (should error).
    
-   Fibonacci: `n=1`, `n=2`, `n=10` → confirm sequence.