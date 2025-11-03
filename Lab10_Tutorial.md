# CSE130 — Lab 10 Tutorial  
**Title:** Extending Tic-Tac-Toe to 3D with Inheritance and OOP  
**Continuation of:** Lab 9 — Tic-Tac-Toe in C++ with OOP  

---

## 🎯 Goal  
In Lab 9, you created a 2D Tic-Tac-Toe game using classes and basic OOP principles.  
In **Lab 10**, you’ll take it further by extending your `TicTacToe` class into a **3D version** — `TicTacToe3D` — using **inheritance**, **virtual functions**, and **method overriding**.  

You’ll learn to:  
- Build on your previous class design.  
- Use inheritance to reuse and extend functionality.  
- Implement 3D game logic with a 3×3×3 grid.  
- Apply object-oriented principles for scalability and clarity.

---

## 🧠 Key Concepts Review

### 1 — Inheritance in C++
Inheritance allows a **derived class** to reuse and expand the functionality of a **base class**.

```cpp
class DerivedClass : public BaseClass {
    // new members or overridden methods
};
```

Here, `TicTacToe3D` will inherit from `TicTacToe`.  

### 2 — Virtual Functions and Overriding  
- Use `virtual` in the base class for methods you want to redefine in derived classes.  
- The derived version **overrides** the base one to implement specialized behavior.  

Example:
```cpp
virtual void displayBoard();
```
In `TicTacToe3D`, we redefine this method to display a 3D board.

---

## 🧩 Step 1 — Updating the Base Class (`TicTacToe`)

You will use your Lab 9 implementation as a base.  
Modify it slightly to support inheritance:  

1. Make `currentPlayer` **protected** (accessible to subclasses).  
2. Mark key methods as **virtual** for overriding.  

```cpp
class TicTacToe {
    char board[3][3];
protected:
    char currentPlayer; // still needed by the derived class

public:
    TicTacToe();
    virtual void displayBoard();
    virtual void playerMove();
    virtual void computerMove();
    virtual bool checkWin();
    bool isFull();
    void switchPlayer();
};
```

This ensures your Lab 10 class can **reuse** most of Lab 9’s logic while replacing or expanding parts of it.

---

## 🧭 Step 2 — Designing the Derived Class (`TicTacToe3D`)

`TicTacToe3D` inherits from `TicTacToe` and adds a new 3×3×3 board.

```cpp
class TicTacToe3D : public TicTacToe {
private:
    char board3D[3][3][3];

public:
    TicTacToe3D();
    void displayBoard() override;
    void playerMove() override;
    void computerMove() override;
    bool checkWin() override;
    bool isFull3D();
    void run3D();
};
```

This design maintains a clean structure and highlights **code reuse through inheritance**.

---

## 🧱 Step 3 — Constructor Initialization

```cpp
TicTacToe3D::TicTacToe3D() {
    for (int z = 0; z < 3; z++)
        for (int i = 0; i < 3; i++)
            for (int j = 0; j < 3; j++)
                board3D[z][i][j] = ' ';

    srand(time(0));
    currentPlayer = (rand() % 2 == 0) ? 'X' : 'O';
    cout << "Player '" << currentPlayer << "' starts first!\n";
}
```

---

## 🧮 Step 4 — Displaying the 3D Board

Each layer represents one 3×3 grid.

```cpp
void TicTacToe3D::displayBoard() {
    for (int z = 0; z < 3; z++) {
        cout << "\nLayer " << z + 1 << ":\n";
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                cout << (board3D[z][i][j] == ' ' ? '_' : board3D[z][i][j]);
                if (j < 2) cout << " | ";
            }
            cout << "\n";
        }
    }
}
```

---

## 🎮 Step 5 — Handling Moves

### Player Move
```cpp
void TicTacToe3D::playerMove() {
    int layer, row, col;
    cout << "Enter layer (1-3), row (1-3), column (1-3): ";
    cin >> layer >> row >> col;

    if (board3D[layer - 1][row - 1][col - 1] != ' ') {
        cout << "Cell already occupied! Try again.\n";
        playerMove();
        return;
    }
    board3D[layer - 1][row - 1][col - 1] = currentPlayer;
}
```

### Computer Move (Random Placement)
```cpp
void TicTacToe3D::computerMove() {
    int layer, row, col;
    do {
        layer = rand() % 3;
        row = rand() % 3;
        col = rand() % 3;
    } while (board3D[layer][row][col] != ' ');

    board3D[layer][row][col] = currentPlayer;
    cout << "Computer plays at Layer " << layer + 1 << ", Row " << row + 1 << ", Col " << col + 1 << "\n";
}
```

---

## 🧩 Step 6 — Win Checking Logic

Winning occurs when a player gets **three in a row** in any dimension:

1. **Within each layer** (horizontal, vertical, or diagonal)  
2. **Across layers** (vertical through the same position)  
3. **Face Diagonals** (across layers)
3. **Through space diagonals** (corner-to-corner)
---

## 🧾 Step 8 — Main Function

```cpp
int main() {
    TicTacToe3D game;
    game.run3D();
    return 0;
}
```

---

## ✅ Checklist  

| Feature | Status |
|----------|---------|
| Reuses Lab 9 code via inheritance | ✅ |
| Implements 3×3×3 board | ✅ |
| Handles illegal moves | ✅ |
| Uses OOP principles | ✅ |
| Detects wins & draws | ✅ |
| Demonstrates overriding | ✅ |

---

## 💡 Optional Enhancements  
- Add scoring (count wins for both players).  
- Colorize output to visualize layers better.  
- Improve computer strategy (block or win moves).

---

**Summary:**  
Lab 10 builds directly on your Lab 9 foundation. You’ll see how inheritance enables code reuse and how overriding lets you create new behavior while keeping your program modular and maintainable. This lab also challenges you to think in 3D — a key step toward more complex simulations and games. 🚀
