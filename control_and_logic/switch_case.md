# Switch - Case Statements

There's another way to handle conditions in C++ - switch and case statements. They overlap with if-else in purpose, but they're a better fit for a specific scenario: checking whether a single variable equals one of several known values.

Say you have an integer and want three different outputs depending on its value. Switch-case handles that cleanly:

```cpp
#include <iostream>

int main() {
    int condition {};

    std::cout << "Choose the condition: ";
    std::cin >> condition;

    switch (condition) {
        // if condition is equal to 0:
        case 0:
            std::cout << "Path 0 is open!\n";
            break;
        // if condition is equal to 1:
        case 1:
            std::cout << "Path 1 is open!\n";
            break;
        // if condition is equal to 2:
        case 2:
            std::cout << "Path 2 is open!\n";
            break;
        // if nothing matches:
        default:
            std::cout << "Invalid!\n";
            break;
    }

    return 0;
}
```

> **Note:** `break` is a jump statement - it kicks the compiler out of the switch block so it doesn't keep running into the next case. We'll cover jump statements properly in the loops chapter. For now, just remember: always end your cases with `break` unless you have a reason not to.

> **Note:** Inside a function, you can also end a case with `return` instead of `break`. That's covered in the functions chapter.

---

So why use switch-case at all? It's mostly a readability win - there's no significant performance difference. But when you're matching a variable against a fixed set of values, switch-case reads much cleaner than a chain of if-else.

One important constraint: **switch-case only works with equality checks.** You can't do `case x > 5:` or anything like that. Think of every case as an implicit `==`. If you need range checks or complex conditions, stick with if-else.

Switch-case works with **integers, chars, and enums**. Here's a char example:

```cpp
#include <iostream>

int main() {
    char condition {};

    std::cout << "Choose a path (x, y, z): ";
    std::cin >> condition;

    switch (condition) {
        // this part will be executed when condition is x
        case 'x':
            std::cout << "Path X is open!\n";
            break;
        // this part is for y
        case 'y':
            std::cout << "Path Y is open!\n";
            break;
        // and for z
        case 'z':
            std::cout << "Path Z is open!\n";
            break;
        // and anything else triggers this part
        default:
            std::cout << "Invalid!\n";
            break;
    }

    return 0;
}
```

> **Note:** Strings (`"x"`, `"y"`) do **not** work in switch-case - that's a compile error. Use single-quoted chars (`'x'`, `'y'`) or integers instead.

> **Editor's note:** Strings are a text type we'll cover later; for now just know that a char holds a single character, while a string holds a sequence of them (words, sentences etc.).

---

## The `[[fallthrough]]` Attribute

Introduced in C++17.

Normally, each case in a switch ends with `break` to stop execution. But if you omit `break`, execution "falls through" into the next case automatically. This is usually a bug - and most compilers will warn you about it.

Sometimes though, fallthrough is exactly what you want. The `[[fallthrough]]` attribute tells the compiler: *this is intentional, don't warn me.*

> *Editor's note:* Fallthrough simply means: if you don't end a case with break or return, execution doesn't stop - it continues into the next case regardless of whether it matches. Normally each case produces one output. Fallthrough lets multiple cases share the same code path.

Example:

```cpp
#include <iostream>

int main() {
    int day {};

    std::cout << "Enter day: ";
    std::cin >> day;

    switch (day) {
        case 1:
            [[fallthrough]]; // intentional — weekdays share the same output
        case 2:
            [[fallthrough]];
        case 3:
            [[fallthrough]];
        case 4:
            [[fallthrough]];
        case 5:
            std::cout << "Weekday. Back to work.\n";
            break;
        case 6:
            [[fallthrough]]; // intentional — weekend days share the same output
        case 7:
            std::cout << "Weekend. Finally.\n";
            break;
        default:
            std::cout << "Invalid day.\n";
            break;
    }

    return 0;
}
```

Output (if input is 3):
```
Weekday. Back to work.
```

Output (if input is 6):
```
Weekend. Finally.
```

`[[fallthrough]]` goes where the `break` would normally be, followed by a semicolon (it replaces the null statement there). It does nothing at runtime - it's purely a signal to the compiler and anyone reading the code that you meant to skip the `break`.

Use it sparingly. Fallthrough can make control flow hard to follow. When you do use it, `[[fallthrough]]` makes the intent explicit.
