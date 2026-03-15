# Return Statements

You've been writing `return 0;` since chapter one without much explanation. Time to actually talk about what's going on.

---

## What a Return Statement Does

A return statement does two things, in order:

1. Evaluates the expression after `return`
2. Sends that value back to whoever called the function, then exits the function immediately

```cpp
int add_four(int x)
{
    return x + 4; // evaluates x + 4, sends result back, then exits
}
```

> *Editor's Note:* Don't mind `int x` inside the parentheses for now - it's a parameter, but I'll explain that in the next chapter. For now, just think of it this way: when you call a function, you can decide what input goes into it.

When `main` calls `add_four(4)`, the function runs, evaluates `3 + 4`, returns `7`, and control goes back to `main`. That `7` is the **return value**.

---

## The Return Type

The type declared before the function name tells the compiler what kind of value this function promises to give back.

```cpp
int    get_value()  { return 42;    } // returns an int
double get_pi()     { return 3.14;  } // returns a double
bool   is_active()   { return true;  } // returns a bool
```

This is a contract. If you declare `int` but don't return anything - undefined behavior. The compiler will usually warn you, but it won't always catch every case. Don't rely on it.

---

## Functions That Return Nothing: `void`

Not every function needs to send something back. If a function just *does* something, prints to screen, modifies a file, you mark its return type as `void`.

```cpp
void print_hi()
{
    std::cout << "Hi\n";
    // no return needed
}
```

`void` functions automatically return to the caller when they reach the end. You can write `return;` with no value to exit early, but putting it at the very end is just noise.

```cpp
void is_positive(int x)
{
    if (x <= 0)
        return;  // early exit - this is fine and useful

    std::cout << x << '\n';
}
```

### What you cannot do with `void`

You can't use a void function where a value is expected.

```cpp
void hi() { std::cout << "Hi\n"; }

int main()
{
    hi();               // fine
    std::cout << hi();  // compile error - there's no value to print
}
```

And you definitely can't return a value from a void function:

```cpp
void broken()
{
    return 5; // compile error
}
```

---

## `main`'s Return Value

`main` returns an `int` - this is non-negotiable in C++. That value is a **status code** sent to the operating system.

| Value | Meaning |
|-------|---------|
| `0` | Program ran successfully |
| Non-zero | Something went wrong |

```cpp
int main()
{
    // ... program logic ...
    return 0; // all good
}
```

`main` is special in one way: if you forget the `return 0;`, the compiler inserts it for you implicitly. Still, write it explicitly. Consistency matters, and it signals intent.

---

## A Function Returns Once

The first `return` the function hits ends it. Everything after is dead code.

```cpp
int get_num()
{
    return 5;
    return 4; // never reached
}
```

This compiles, but `4` is never returned. Ever. The function always returns `5`.

---

## The Caller Decides What to Do With the Value

Returning a value doesn't mean it gets used. The caller can use it, ignore it, or pass it along.

```cpp
int mystery() { return 42; }

int main()
{
    int x = mystery();       // stored
    std::cout << mystery();  // used directly
    mystery();               // returned value discarded
}
```

That's all !
