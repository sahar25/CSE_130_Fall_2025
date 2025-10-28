# CSE130 — Lab 9 Tutorial  
**Title:** Tic-Tac-Toe in C++ with OOP  
**Goal:** Build a Tic-Tac-Toe game that plays against the computer using Object-Oriented Programming (OOP) concepts.

---

## 1. What You’ll Learn
- How to design and implement a **C++ class**.  
- Use of **constructors**, **member functions**, and **data encapsulation**.  
- Randomizing who starts the game.  
- Validating user input and detecting **win**, **draw**, or **illegal moves**.  

---

## 2. Problem Description
Create a 3 × 3 Tic-Tac-Toe game where:
- The **board** is printed using ASCII symbols.  
- The program randomly decides who starts (user or computer).  
- If the player chooses an already occupied cell, print an error and **re-ask**.  
- The program must detect and print whether someone **wins** or if it’s a **draw**.  
- Use at least **one class** (for the game).  

---

## 3. Program Design

We’ll use **one main class** that keeps track of the board and game logic.

```
+-------------------+
|    TicTacToe      |
|-------------------|
| - board[3][3]     |
| - currentPlayer   |
|-------------------|
| +TicTacToe()      |
| +displayBoard()   |
| +playerMove()     |
| +computerMove()   |
| +checkWin()       |
| +isFull()         |
| +switchPlayer()   |
| +run()            |
+-------------------+
```
**We can also have a different design where we create a separate class for the board or/and the players.**
---

## 4. Step-by-Step Implementation

### Step 1 — Include Libraries
We’ll use only the standard libraries needed for console I/O and random numbers.

```cpp
#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;
```

### Step 2 — Define the Class(es)
```cpp
class TicTacToe {
    char board[3][3];
    char currentPlayer;

public:
    TicTacToe();           // constructor
    void displayBoard();   // show the board
    void playerMove();     // user move
    void computerMove();   // computer move
    bool checkWin();       // did anyone win?
    bool isFull();         // is the board full?
    void switchPlayer();   // switch X ↔ O
    void run();            // main game loop
};
```

---

## 5. Implementation Details

### Constructor
Initializes the empty board and picks a random starting player.

```cpp
TicTacToe::TicTacToe() {
    for (int i=0;i<3;i++)
        for (int j=0;j<3;j++)
            board[i][j] = ' ';

    srand(time(0));
    currentPlayer = (rand() % 2 == 0) ? 'X' : 'O';
    cout << "Player '" << currentPlayer << "' starts first!\n";
}
```

### Displaying the Board
```cpp
void TicTacToe::displayBoard() {
    cout << "\n";
    for (int i=0;i<3;i++) {
        for (int j=0;j<3;j++) {
            cout << (board[i][j] == ' ' ? '_' : board[i][j]);
            if (j < 2) cout << " | ";
        }
        cout << "\n";
    }
    cout << "\n";
}
```

### Switch Player
```cpp
void TicTacToe::switchPlayer() {
    currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
}
```
---

## 6. Main Function
```cpp
int main() {
    TicTacToe game;
    game.run();
    return 0;
}
```

---

## 7. Checklist
✅ Randomly selects starting player  
✅ Prevents illegal moves  
✅ Detects win and draw  
✅ Uses at least one class (OOP)  

---

## 8. Optional Ideas
- Replace random computer moves with a **blocking strategy**.  
- Add colored output or ASCII art for fun. 

---

**Keep it simple, test often, and have fun! 🧩**