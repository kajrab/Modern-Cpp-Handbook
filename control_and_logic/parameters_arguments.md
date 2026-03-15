# Function Parameters and Arguments

Parameters are how you talk to a function. Arguments are what you actually say.

Didn't get it? Let's try again:

Parameters are inputs that only exist inside a function. Arguments are the values you provide for those parameters.

Still not clear? One more time:

```
f(x) = 2x + 1
f(3) = 7
```

`x` is a parameter - the desired input. `3` is an argument - the given input.

That should be enough to get the concept.

## 1. Parameters vs. Arguments 

These two words get mixed up constantly. They refer to different things at different points in a function's lifetime.

| Term | What it is |
|---|---|
| **Parameter** | A named variable declared in the function signature. It receives a value when the function is called. |
| **Argument** | The actual value passed in at the call site. It gets copied into the parameter. |

Think of a parameter as an **empty box** the function defines, and an argument as the **item you put inside it** each time you call the function.

---

## 2. Defining Parameters in a Function

Parameters are declared inside the parentheses of a function definition. Each one needs a type and a name, separated by commas if there are multiple.

```cpp
// Two parameters: x and y, both of type int
void sum(int x, int y)
{
    std::cout << x + y << '\n';
}
```

`x` and `y` exist **only inside the body of `sum`**. They are created when the function is entered and destroyed when it returns. You cannot access them from outside.

> **Editor's Note:** A parameter's lifetime is tied to a single function call. Every time you call `sum()`, fresh copies of `x` and `y` are created, used, and discarded. They have no memory of previous calls.

---

## 3. Passing Arguments When Calling a Function

When you call a function, you supply arguments in the same order as the parameters were declared. By default, C++ **copies** the argument value into the parameter, this is called *pass-by-value*.

```cpp
int main()
{
    sum(5, 4);    // 5 is copied into x, 4 is copied into y → prints 9
    sum(12, 8);   // now x = 12, y = 8 → prints 20
    return 0;
}
```

The caller decides the values. The function doesn't care where they come from - literals, variables, or expressions all work the same way.

```cpp
int a = 3;
int b = 7;
sum(a, b);         // variables as arguments     → x = 3, y = 7
sum(a + 1, b * 2); // expressions as arguments   → x = 4, y = 14
```

---

## 4. Using a Function's Return Value as an Argument

A function's return value can be passed directly as an argument to another function. The inner call runs first, and its return value is handed straight to the outer call - no temporary variable needed.

```cpp
#include <iostream>

int get_int()
{
    std::cout << "Enter an integer: ";
    int input {};
    std::cin >> input;
    return input;
}

void print_int(int value)
{
    std::cout << "The value is: " << value
              << ", and value + 4 is: " << value + 4 << '\n';
}

int main()
{
    print_int(get_int());   // get_int() runs first, result fed directly to print_int()
    return 0;
}
```

**Output:**

```
Enter an integer: 6
The value is: 6, and value + 4 is: 10
```

`print_int(get_int())` evaluates right-to-left at the argument level: `get_int()` runs, returns its `int`, and that value is immediately used as the argument to `print_int()`. Clean, no clutter.

> **Editor's Note:** Composing function calls like this removes the need for throwaway temporary variables. You will see this pattern constantly in real C++ codebases.

---

## 5. Unreferenced Parameters and Unnamed Parameters

Sometimes you need a function to match a specific signature; because an interface, callback, or virtual function requires it - but you don't actually use one of the parameters inside the body. C++ gives you two ways to handle this cleanly.

### The Problem: Unused Parameter Warning

If you name a parameter but never use it, most compilers will warn you. That warning usually means you forgot something - but occasionally the unused parameter is intentional.

```cpp
void on_event(int event_code, int flags)  // flags is never used
{
    std::cout << "Event: " << event_code << '\n';
    // compiler may warn: unused parameter 'flags'
}
```

### Solution A: Cast to `void`

Explicitly casting the unused parameter to `void` tells the compiler you know it's there and are intentionally ignoring it.

```cpp
void on_event(int event_code, int flags)
{
    (void)flags;   // suppresses the unused-parameter warning
    std::cout << "Event: " << event_code << '\n';
}
```

### Solution B: Unnamed Parameters (Preferred)

The cleaner, idiomatic C++ approach is to simply **omit the parameter name**. You keep the type in the signature so the interface is satisfied, but give it no name; which silences the warning automatically and makes it impossible to accidentally use.

```cpp
void on_event(int event_code, int //flags)
{
    std::cout << "Event: " << event_code << '\n';
}
```

Writing the name inside a comment, like `//flags`,is the standard convention. It keeps the code readable (anyone can see what the parameter represents) without triggering a warning.

> **Editor's Note:** Unnamed parameters are common in callbacks, event handlers, and virtual function overrides where the signature is fixed by an external interface but your implementation doesn't need all the data. They also appear in operator overloads; the postfix `++` operator takes an unnamed `int` purely to distinguish it from prefix.
