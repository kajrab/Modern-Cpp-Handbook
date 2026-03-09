# Goto Statement

`goto` is a jump statement that lets you teleport to a labeled point anywhere in your code. The label is just a name followed by a colon; you place it wherever you want to land, and `goto` jumps straight there when it is hit.

```cpp
#include <iostream>

int main() {
    int age {};

    std::cout << "Enter your age: ";
    std::cin >> age;

    if (age < 0 || age > 150) {
        goto invalid; // jumps to the label below
    }

    std::cout << "Your age is: " << age << "\n";
    return 0;

invalid: // label
    std::cout << "That's not a valid age.\n";
    return 1;
}
```

> **Editor's note:** Labels follow their own scoping rules and are visible throughout the entire function they are defined in; not just below where they appear.

---

## Why you should avoid it

Main reason why is: It breaks the natural top-to-bottom flow of a program and makes it genuinely hard to trace what is happening; especially once the codebase grows. Code that jumps around arbitrarily is notoriously difficult to read and debug. This is what people mean by the term **spaghetti code** ,if you drew arrows between every `goto` and its label across a large file, it would look exactly like that.

Everything `goto` can do, structured alternatives do better:
1. Repeating logic; use loops. 
2. Handling invalid input; use if-else. 
3. Exiting early; use `return` or `break`.

> **Editor's note:** You will still encounter `goto` in older codebases and C code. Just know what it does and do not reach for it yourself. Unless...

---

## The one case where `goto` is actually fine

Breaking out of nested loops. `break` only exits the innermost loop, so without `goto` you would need an extra flag variable or a full restructure just to escape multiple levels at once. `goto` handles it cleanly:

```cpp
#include <iostream>

int main() {
    for (int i = 0; i < 5; i++) {
        for (int j = 0; j < 5; j++) {
            if (i + j == 6) {
                goto done; // exits both loops at once
            }
            std::cout << i << "," << j << "\n";
        }
    }

done:
    std::cout << "Stopped at i + j == 6.\n";
    return 0;
}
```
