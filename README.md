# Square-Number-Increasing-Pattern



```cpp
#include <bits/stdc++.h>

using namespace std;

int main() {
    int n;
    cin >> n;
    int a = 1;  // Counter variable initialized to 1

    for (int i = 0; i < n; i++) {            // Outer loop: runs n times (for each row)
        for (int j = 0; j < n; j++) {        // Inner loop: runs n times (for each column)
            cout << a << " ";               // Print current value of 'a'
            a = a + 1;                      // Increment 'a' by 1
        }
        cout << endl;                       // After each row, move to the next line
    }
}
```

### What does this code do?

If the user inputs a number `n`, this code prints an `n x n` grid of incrementing integers starting from 1.

#### Example input:

```
3
```

#### Output:

```
1 2 3 
4 5 6 
7 8 9 
```

---

### Why is `a` declared **outside** the outer loop?

Declaring `a` outside the loop allows it to **retain its value across all iterations of the outer loop**. So it keeps counting upward as you go row by row.

---

### What happens if you declare `a` **inside** the outer loop?

If you write:

```cpp
for (int i = 0; i < n; i++) {
    int a = 1;
    for (int j = 0; j < n; j++) {
        cout << a << " ";
        a = a + 1;
    }
    cout << endl;
}
```

Then `a` is **re-initialized to 1** at the beginning of **every row**, so the output will be:

```
1 2 3 
1 2 3 
1 2 3 
```

In this case, `a` does **not** retain its previous value between rows.

---

### Summary

* Declaring `a` **outside** the outer loop lets it count continuously from 1 to `n*n`.
* Declaring `a` **inside** the outer loop resets it to 1 at the beginning of each row.





---

### 🔍 Why does `a` behave differently depending on where it's declared?

It’s all about **where the variable is declared** — which determines its **lifetime** and **visibility**, i.e., its **scope**.

---

### 🔁 Case 1: `a` declared **outside** the outer loop

```cpp
int a = 1; // Declared before any loops

for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        cout << a << " ";
        a = a + 1;
    }
    cout << endl;
}
```

* **Scope of `a`**: From the point it's declared until the end of the `main()` function.
* It gets created once, keeps its value through all iterations.
* So, it starts at 1 and just keeps increasing with every print.

---

### 🔁 Case 2: `a` declared **inside** the outer loop

```cpp
for (int i = 0; i < n; i++) {
    int a = 1;  // Declared inside the loop — a **new `a`** each time

    for (int j = 0; j < n; j++) {
        cout << a << " ";
        a = a + 1;
    }
    cout << endl;
}
```

* **Scope of `a`**: Only inside the current iteration of the outer loop.
* Every time the outer loop starts a new iteration (a new row), a **new variable `a`** is created and set to `1`.
* So each row starts with `1`, producing rows like `1 2 3`.

---

### 📌 Why exactly does this happen?

Because in C++, **variables declared inside a block (`{}`)** only exist for the duration of that block. When the outer `for` loop ends one iteration, the block ends, and `a` gets **destroyed**. On the next iteration, a **new copy of `a`** is created again.

This is how C++ manages memory and scope — it’s deterministic and based on block structure.

---

### ✅ Rule of Thumb

* Declare a variable **outside a loop** if you want it to **persist** across multiple loop iterations.
* Declare it **inside a loop** if it should **reset/restart** with each iteration.

