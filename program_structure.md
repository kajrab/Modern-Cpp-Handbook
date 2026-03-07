# Anatomy of a C++ Program
Welcome to the world of C++. This guide started a bit weird, I know; we covered variables, literals, operators, expressions, statements, and I/O, but we never talked about something we kept seeing in the I/O chapter:
```cpp
#include <iostream>  // library
int main() {         // entry point
    std::cout << "Hello, World!";  // statement
    return 0;        // exit code
}
```
You might be wondering: what the heck is `int main()` or `return 0`? Because those are actually the only things here you don't know yet. You already know how to include a library from the I/O chapter and you know `cout` itself from the same place.

So what is `int main() {}`? It's a function. Think of it as a starter function. Everything begins when `main()` runs, and your statements execute inside it, in order. When your compiler sees `int main()`, it says "program started" and works through the statements one by one.

`int` means this function must return a number. Why an integer? Your OS wants an exit code, and exit codes are numbers. So `int` is the return type, and `main` is the function's name.

And `return 0;` — you probably already figured it out. If our function has to produce an integer as output, we have to return it. `return` is a statement that jumps back to whoever called the function. In `main`'s case, that's the OS.

Here's a function structure to make it clear:

```cpp
int function_name() {
    // statements!
    return 404; // random, but valid
}
```

`int` here means the function must return an integer. Swap it for `float` and it must return a float instead. That's the return type — it tells the compiler what kind of value comes out. We'll go deeper on functions later; just hold onto the concept for now.

---

So stepping back to the full picture:

```cpp
#include <iostream>
int main() {
    return 0;
}
```

1. `#include <iostream>` — pulls in the library so we can use `cout`
2. `int main()` — program starts
3. `return 0` — program exits

Anything you add between the curly braces before `return 0;` will run.
