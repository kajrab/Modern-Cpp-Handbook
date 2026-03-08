# Expressions
An expression is anything that evaluates to a value. That value can be a number, a boolean, a character; anything.

```cpp
2 + 3        // evaluates to 5
x = 4 + 5   // evaluates to 9, then assigns it to x
++x          // evaluates to x + 1, then updates x
x > 0        // evaluates to true or false
```

The key idea — every expression has two jobs: **produce a value** and sometimes **cause a side effect** (like changing a variable). `++x` does both; it gives you the new value and actually modifies x.

Expressions can be as simple as a single literal like `5`, or nested and complex like `(x * 2) + (y - 1)`. As long as it resolves to a value, it's an expression.

Note: Expressions can't run by themselves — they have to live inside a [statement](statement.md). Slap a semicolon on one and it becomes a statement. `x + 1` is an expression. `x + 1;` is now a statement; technically valid but useless since you're not doing anything with the result.
