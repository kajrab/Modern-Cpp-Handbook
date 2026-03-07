# IO Basics

IO stands for input and output, and it is essential for anyone who wants to get input from the user and display something back.

For console applications we use the `iostream` library. It handles basic input and output and is part of the C++ standard library, so there is nothing extra to set up.

```cpp
#include <iostream>
```

Include it at the top of your file before using anything from it.

---

## std::cout

`std::cout` (character output) sends data to the console using the insertion operator `<<`.

> If you are not a beginner: `std::` is the standard namespace prefix, and `<<` is the insertion operator. It is overloaded, meaning the same symbol works differently depending on context; you can even define your own custom output behavior for your own types, but that is a topic for later.

```cpp
#include <iostream>

int main()
{
    std::cout << "Hello, world!"; // prints text
    std::cout << 44;              // prints a number

    int num { 5 };
    std::cout << num;             // prints the value of a variable

    return 0;
}
```

You can chain multiple `<<` operators in one statement:

```cpp
std::cout << "number is equal to: " << num << '\n';
```

Separate `std::cout` statements do not automatically print on separate lines, you have to handle newlines yourself.

---

## Newlines: `\n` vs `std::endl`

Both move the cursor to the next line, but they behave differently under the hood.

`std::endl` does two things: outputs a newline and flushes the output buffer. `\n` only outputs a newline without flushing.

```cpp
std::cout << "Hello" << std::endl; // newline + flush (slower)
std::cout << "Hello" << '\n';      // newline only (faster)
```

`endl` is slower because of the flush. The upside is that it guarantees output is written immediately, so if your program aborts before the buffer gets a chance to flush on its own, you do not lose anything. That makes it useful for debugging, but overkill in normal code.

Editor note: I sometimes use endl out of habit but don't do that.

### What is the buffer?

> Feel free to skip this section if you are just getting started. It is a gentle introduction, and nothing later depends on fully understanding it right now.

> **Editor note:** I still recommend reading this part carefully, it is not that confusing. Maybe a little if you are just starting out, but I tried to make it as approachable as possible.

Output sent to `std::cout` does not go directly to the screen. It first sits in a region of memory called a **buffer**, and gets sent out in batches. Think of it like a holding area, data accumulates there, and the system sends it all at once when the time is right. 

This is more efficient than writing each character to the screen the moment it is produced.

Flushing means forcing everything currently in the buffer to be sent to its destination right now.

> **Editor note:** Once your data is sent to the destination, the buffer resets.

A useful analogy: instead of making a delivery trip for every single item, you load everything into a truck first and make one trip. The buffer is the truck. Flushing is when it drives off.

`std::endl` triggers a flush every single time it is used. In a tight loop, that adds up fast:

```cpp
// slow — flushes 1000 times
for (int i = 0; i < 1000; ++i)
    std::cout << "New " << i << std::endl;

// fast — buffer flushes on its own schedule
for (int i = 0; i < 1000; ++i)
    std::cout << "New " << i << '\n';
```

C++'s output system is designed to flush itself periodically, and it flushes automatically when the program exits cleanly. So in most cases, just let it do its thing and use `'\n'`.

Reach for `std::endl` only when you specifically need a guaranteed immediate flush; debugging a crash, writing to a file or socket, or making sure a prompt appears before waiting on user input.

**Quoting convention:** when `\n` stands alone, use single quotes (`'\n'`). When it is embedded inside a string literal, it stays in the double quotes.

```cpp
std::cout << "x is: " << x << '\n';      // standalone — single quotes
std::cout << "And that's all, folks!\n"; // embedded — inside the string
```

---

## std::cin

`std::cin` (character input) reads from the keyboard using the extraction operator `>>`.

Notice the direction: `<<` is for insertion (output), `>>` is for extraction (input). They are just operators, like `+` or `-`; the angle brackets point toward where the data is going.

```cpp
#include <iostream>

int main()
{
    std::cout << "Enter a number: ";

    int num {};       // always initialize before use
    std::cin >> num; // extracts input and stores it in num

    std::cout << "Your number is " << num << '\n';
    return 0;
}
```

You can chain extractions the same way you chain output:

```cpp
int x {}, y {};
std::cin >> x >> y; // reads two values, separated by whitespace
```

### How the input buffer works

> Same deal; skip if you want, but it is worth knowing eventually.

Input is also buffered. When you type and press Enter, your input goes into the input buffer as a character sequence with `'\n'` appended at the end. 

The extraction operator `>>` then pulls characters from the front of that buffer, skips any leading whitespace, and stops when it hits a character that does not match the target type.

Leftover characters stay in the buffer for the next extraction:

```cpp
// user enters: 4 5
std::cin >> x; // extracts 4, leaves " 5\n" in the buffer
std::cin >> y; // extracts 5 from what's left — does not wait for new input
```

### What happens when extraction fails

If the input does not match the variable's type;  for example, the user enters letters when an `int` is expected; extraction fails. The variable gets set to `0`, and `std::cin` enters a failed state where all future extractions silently do nothing (but still set your variables to 0) until you explicitly clear it.

```cpp
int x {};
std::cin >> x; // user enters "kai" — extraction fails, x = 0
```

Example with chained extractions:

```cpp
int x {} , y {};
std::cin >> x >> y;

std::cout << x << y;

// Output: 00
```

`std::cin` just hardcodes that behavior on failure. It comes and says: "I couldn't extract anything, so I'll set your variable(s) to `0` and call it a day."

A few edge cases worth knowing:

`"3.14"` into an `int` — extracts `3`, leaves `.14` in the buffer  
`"123abc"` into an `int` — extracts `123`, leaves `abc` in the buffer  
`"abc123"` into an `int` — fails immediately, `x = 0`

Proper error handling for `std::cin` (detecting failure, clearing state, discarding bad input) is covered separately.

---

## Operator Direction Reference

| Expression       | Meaning                                  |
|------------------|------------------------------------------|
| `std::cout << x` | send `x` to the console                  |
| `std::cin >> x`  | read from keyboard into `x`              |
| `<<`             | insertion — data flows toward output     |
| `>>`             | extraction — data flows toward variable  |

Think of the operators as arrows pointing in the direction data travels.

---

> **Editor note:** I know this feels like a lot for a basic IO chapter, and the buffer section might seem unnecessary this early; but it is essential groundwork for later concepts in C++. And buffer mismanagement is one of the most common sources of security vulnerabilities in C++ programs, so it is not something you can just skip over.
