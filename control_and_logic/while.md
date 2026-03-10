# While Loops

Loops are how you make code repeat. Instead of writing the same logic five times, you write it once and tell the program to keep running it until some condition is no longer true.

The `while` loop is the simplest form of that idea:

```cpp
while (condition) {
    // runs as long as condition is true
}
```

Before each iteration, the condition is checked. If it's true, the body runs. If it's false, execution moves on. If the condition is already false from the start, the body never runs at all.

Here's a basic example:

```cpp
#include <iostream>

int main() {
    int count { 0 };

    while (count < 5) {
        std::cout << "count is: " << count << '\n';
        count++; // increment, or this runs forever
    }

    return 0;
}
```

Output:
```
count is: 0
count is: 1
count is: 2
count is: 3
count is: 4
```

The loop runs while `count < 5`. Each iteration prints the value and bumps it up by one. When `count` hits 5, the condition fails and the loop exits.

> **Editor's Note:** `count++` is the prefix increment operator, it adds 1 to `count`. We covered this in the operators chapter.

---

## Infinite Loops

If the condition never becomes false, the loop never stops. That's an infinite loop:

```cpp
while (true) {
    // runs forever
}
```

`while (true)` is the standard way to write one intentionally. It's not inherently bad, infinite loops are actually useful when you want something to keep running until an explicit exit condition is hit from inside the loop.

A common pattern is a menu that keeps prompting until the user chooses to quit:

```cpp
#include <iostream>

int main() {
    int choice {};

    while (true) {
        std::cout << "1. Play\n";
        std::cout << "2. Quit\n";
        std::cout << "Enter choice: ";
        std::cin >> choice;

        if (choice == 2) {
            std::cout << "Good bye.\n";
            break; // exits the loop
        }

        if (choice == 1) {
            std::cout << "Starting game...\n";
        } else {
            std::cout << "Invalid choice.\n";
        }
    }

    return 0;
}
```

The loop keeps running until the user enters `2`, which hits `break` and exits. Everything else either starts the game or complains about the input.

> **Editor's Note:** `break` was mentioned back in the switch-case chapter. Here it does the same thing, jumps out of the enclosing block, which in this case is the `while` loop. Next chapter you are gonna learn more about it so do not worry!

Unintentional infinite loops are a different story. If you forget to update whatever the condition depends on, your program just hangs. Always make sure something inside the loop can eventually make the condition false or that you have a `break` path when using `while (true)`.
