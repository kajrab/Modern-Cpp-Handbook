# If, Else, and Else If

Conditional statements let a program make decisions at runtime; executing different code paths depending on whether a condition is true or false. In C++, the primary tool for this is the `if` statement and its companions: `else` and `else if`.

In other words, they give the user alternate paths. Different inputs trigger different outputs based on conditions you define.

---

## The `if` Statement

The simplest form. Executes a block of code only if the condition evaluates to `true`.

```cpp
if (condition) {
    // executes only when condition is true
}
```

A condition is any expression that evaluates to a boolean (`true` or `false`). This includes comparisons, boolean variables, and anything that produces a boolean result.

```cpp
int score = 85;

if (score >= 60) {
    std::cout << "You passed.\n"; // executes because 85 >= 60 is true
}
```

If the condition is false, the block is skipped and execution continues after the closing brace.

---

## The `else` Clause

Adds a fallback block that executes when the `if` condition is `false`. Exactly one of the two blocks will always execute; never both, never neither.

It runs whenever your `if` doesn't.

```cpp
if (condition) {
    // runs when condition is true
} else {
    // runs when condition is false
}
```

```cpp
int x = 3;

if (x > 10) {
    std::cout << "Greater than 10.\n";
} else {
    std::cout << "Not greater than 10.\n"; // this executes
}
```

---

## The `else if` Chain

Used when there are more than two possible outcomes. Conditions are evaluated top-to-bottom; as soon as one matches, its block runs and the rest are skipped entirely.

Be careful here: sometimes two separate `if` statements are what you actually want, not an `else if` chain. If the conditions aren't mutually exclusive, `else if` will silently skip checks that should have run.

```cpp
if (condition1) {
    // runs if condition1 is true
} else if (condition2) {
    // runs if condition1 is false AND condition2 is true
} else if (condition3) {
    // runs if condition1 and condition2 are false AND condition3 is true
} else {
    // none of the above matched
}
```

The final `else` is optional. Order matters; put the most specific or most likely conditions first.

```cpp
int x {};
std::cin >> x;

if (x > 0) {
    std::cout << "Positive.\n";
} else if (x < 0) {
    std::cout << "Negative.\n";
} else {
    std::cout << "Zero.\n"; // x was exactly 0, the one nobody checks for
}
```

---

## Conditions and Boolean Expressions

The condition inside `if (...)` must evaluate to a boolean. C++ will implicitly convert non-boolean types:

| Condition type | Treated as `true` when |
|---|---|
| Integer | Non-zero |
| Pointer | Non-null |
| bool | true |

You can store conditions in named boolean variables to improve readability; especially useful when the same condition is reused or when the expression is complex.

```cpp
int age      = 20;
bool isAdult = age >= 18;
bool hasID   = true;

if (isAdult && hasID) {
    std::cout << "Access granted.\n";
}
```

> **Editor's note:** `==`, `>=`, `<=` etc. are all comparison operators. Inside a condition, always use `==` to check equality; never `=`. Using `=` is assignment; it will silently overwrite your variable instead of comparing it.

---

## Nested `if` Statements and the Dangling `else` Problem

You can place an `if` statement inside another `if`'s body. This is called nesting.

The **dangling else** problem arises when braces are omitted and it becomes ambiguous which `if` an `else` belongs to. In C++, an `else` always matches the **nearest unmatched `if`**.

```cpp
// AMBIGUOUS: looks like the else belongs to the outer if — it does not
if (x >= 0)
    if (x <= 20)
        std::cout << "Between 0 and 20.\n";
    else
        std::cout << "Negative.\n"; // actually belongs to the inner if
```

Passing `x = 25` here prints "Negative"; which is obviously wrong. Fix it with explicit braces:

```cpp
if (x >= 0) {
    if (x <= 20) {
        std::cout << "Between 0 and 20.\n";
    } else {
        std::cout << "Greater than 20.\n"; // belongs to inner if
    }
} else {
    std::cout << "Negative.\n"; // belongs to outer if
}
```

Nested `if` statements can often be **flattened** using logical operators:

```cpp
// Nested
if (x >= 0) {
    if (x <= 20) {
        std::cout << "In range.\n";
    }
}

// Flattened; same logic, much cleaner
if (x >= 0 && x <= 20) {
    std::cout << "In range.\n";
}
```

---

## `if` with Init-Statement (C++17)

Since C++17, you can declare and initialize a variable directly inside the `if` condition. The variable's scope is limited to the `if`/`else` block; it ceases to exist after.

```cpp
if (int result = computeScore(); result > 0) {
    std::cout << "Score: " << result << '\n';
} else {
    std::cout << "Bad score: " << result << '\n';
}
// result is out of scope here; gone... like her
```

This pattern keeps the surrounding scope clean when you only need a variable for a single conditional check.

---

## `if constexpr` (C++17)

A compile-time conditional. Unlike a regular `if`, only the branch whose condition is `true` **at compile time** gets compiled; the other branch is completely discarded before your program even runs.

> **Editor's note:** The full power of `if constexpr` shows up when writing template functions; a concept covered later. For now, understand what it does and why it exists. Come back to this section after reading the Functions and Templates chapters.

The key distinction from a regular `if`:

```cpp
// Regular if: BOTH branches are compiled, even if only one runs
if (someCondition) {
    // compiled regardless
} else {
    // also compiled regardless
}

// if constexpr: only the matching branch is compiled
if constexpr (someCompileTimeCondition) {
    // compiled ONLY if condition is true at compile time
} else {
    // compiled ONLY if condition is false at compile time
}
```

Think of it like this: a regular `if` is checked at runtime, after the program is already built. `if constexpr` is checked earlier; the compiler reads the condition, picks the correct branch, and throws the other one away before building anything. The discarded branch never makes it into your program at all.

A good example is platform-specific code:

```cpp
#include <iostream>

constexpr bool onWindows = false; // set by your build system

int main() {
    if constexpr (onWindows) {
        std::cout << "Using Windows API\n";
        // this entire block is gone from the binary on non-Windows builds
    } else {
        std::cout << "Using POSIX API\n";
    }

    return 0;
}
```

`onWindows` is known at compile time, so the compiler picks one branch and deletes the other. The Windows code literally does not exist in the Linux build. With a regular `if`, both branches would always compile which becomes a problem the moment one branch calls a platform-specific function that doesn't exist on the other platform. 

Game engines use this pattern constantly: PC vs console, debug vs release, 32-bit vs 64-bit.

---

## Quick Reference

```cpp
// Basic if: runs the block or skips it
if (score >= 60) {
    std::cout << "Passed.\n";
}

// if / else: one or the other, always
if (isOnline) {
    fetchData();
} else {
    loadCache();
}

// if / else if / else: first match wins, rest are ignored
if (grade >= 90)      { std::cout << "A\n"; }
else if (grade >= 80) { std::cout << "B\n"; }
else if (grade >= 70) { std::cout << "C\n"; }
else                  { std::cout << "Study harder.\n"; }

// Nested: inner if inside outer if (use braces to avoid dangling else)
if (isLoggedIn) {
    if (hasPermission) { showDashboard(); }
    else               { showError(); }
}

// C++17: init-statement scopes the variable to the if/else block
if (int val = getValue(); val > 0) {
    use(val);
}

// C++17: compile-time branch, one side never reaches the binary
if constexpr (compileTimeCondition) {
    // compiled in
} else {
    // compiled out
}
```
