# Statements
A statement is a complete instruction that tells the program to do something. Unlike expressions, statements don't evaluate to a value, they just *act*.

```cpp
int x = 5;          // declaration statement
x = x + 1;         // expression statement
if (x > 0) { }     // selection statement
for (int i = 0; i < 10; i++) { }  // iteration statement
return 0;           // jump statement
```

Statements are the building blocks of a program. Every line that actually *does* something is a statement.

There are a few types worth knowing:

**Declaration statements;** introduce a variable into existence. `int x = 5;` tells the program "hey, x exists and it starts at 5."

**Expression statements;** an expression with a semicolon slapped on it. `x = x + 1;` is just the expression `x = x + 1` turned into a statement.

**Selection statements;** `if`, `else`, `switch`. They make decisions.

**Iteration statements;** `for`, `while`, `do while`. They repeat things.

**Jump statements;** `return`, `break`, `continue`. They move control somewhere else.

The simplest statement is a **null statement**, just a lone semicolon `;`. It does nothing, but it is valid.

Note: Statements are where expressions live. See [expressions](expression.md), they need a statement to actually run.
