# Do-While Loop

A `do-while` loop is like a `while` loop with one key difference; the body runs first, then the condition is checked. This guarantees the body executes at least once, no matter what.

> *Editor's Note:* Do-while loops are mostly overlooked because they're basically just while loops with a single extra rule. Do they work? Yeah. Are they that important? Personally, I don't think so.

---

## Syntax

```cpp
do {
    // body
} while (condition);
```

Note the semicolon after the closing parenthesis. Easy to forget.

---

## Basic example

```cpp
int i = 0;

do {
    std::cout << i << ' ';
    ++i;
} while (i < 5);

// output: 0 1 2 3 4
```

This behaves the same as a regular `while` here. The difference shows when the condition is false from the start.

---

## The key difference from while

```cpp
int i = 10;

// while loop - body never runs
while (i < 5) {
    std::cout << i << ' ';
}
// output: (nothing)

// do-while loop - body runs once regardless
do {
    std::cout << i << ' ';
} while (i < 5);
// output: 10
```

The `while` checks before entering. The `do-while` checks after. That one difference is everything.

---

## When to use it

The classic use case is input validation; you always want to ask at least once, then keep asking until you get a valid response.

```cpp
int input;

do {
    std::cout << "Enter a number between 1 and 10: ";
    std::cin >> input;
} while (input < 1 || input > 10);  // keep looping if input is invalid
```

Without `do-while` you'd have to either duplicate the prompt before the loop or use a flag. This is cleaner.

```cpp
int input;

while(true){
  std::cout << "Enter a number between 1 and 10: ";
  std::cin >> input;

  if(input < 1 || input > 10) break;
}
```

It's basically the same thing. do-while just reads a bit more naturally for this pattern but it's not like it's irreplaceable.

---

## With break and continue

`break` exits the loop early. `continue` jumps to the condition check, same as `while`, so make sure your update logic runs before `continue` or you risk an infinite loop.

```cpp
int i = 0;

do {
    ++i;                          // update before continue
    if (i % 2 == 0) continue;    // skip even numbers
    std::cout << i << ' ';
} while (i < 10);

// output: 1 3 5 7 9
```

> *Editor's Note:* Break and continue will be covered in a dedicated chapter later, so don't worry!

---

## Quick reference

| Feature                  | do-while                          |
|--------------------------|-----------------------------------|
| Condition checked        | after the body                    |
| Minimum executions       | 1                                 |
| Semicolon after `while`  | required                          |
| Supports break/continue  | yes                               |
