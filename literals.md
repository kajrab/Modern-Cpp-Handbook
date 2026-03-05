# Literals in C++

Literals are fixed values written directly in source code; not stored in memory locations like variables, just baked right into the executable.

```cpp
char c {'c'};
std::cout << c << std::endl;   // prints the value of a variable
std::cout << 'c' << std::endl; // prints a literal directly
```

Single quotes `' '`, double quotes `" "`, and raw numbers are all literals.

## Literals vs Variables

| | Literals | Variables / Objects |
|---|---|---|
| **Storage** | Compiled directly into the executable | Represent memory locations |
| **Access** | Used as-is | Values fetched at runtime |
| **Mutability** | Fixed, never change | Can be modified |

## Common Literal Types

| Type | Example |
|---|---|
| Integer | `42`, `0xFF`, `0b1010` |
| Float | `3.14f`, `3.14` |
| Character | `'a'`, `'\n'` |
| String | `"hello"` |
| Boolean | `true`, `false` |
| Nullptr | `nullptr` |

> Literals are optimized aggressively by the compiler and may not even appear as distinct values in the final binary.
