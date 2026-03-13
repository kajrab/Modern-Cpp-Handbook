# Functions

Functions are one of the best parts of C++. They improve readability, reduce repetition, and keep your code organized.

---

## Anatomy of a Function

```cpp
returnType functionName()  // Function header
{
    // Function body
}
```

- **Function header:** tells the compiler the function exists and what it returns
- **Function body:** tells the compiler what the function actually does

---

## Breaking Down `main()`

You already know `main()` - it was the first function you ever wrote. Let's use it to understand the syntax:

```cpp
int main() {
    return 0;
}
```

| Part | Meaning |
|------|---------|
| `int` | The return type - this function returns an integer |
| `main` | The function name |
| `return 0` | The value being returned (0 means the program ran successfully) |

---

## More Function Examples

Functions can return different types depending on what you need:

```cpp
// Returns an integer
int getScore() {
    return 100;
}

// Returns a single character
char getGrade() {
    return 'A';
}

// Returns nothing, just performs an action
void greet() {
    std::cout << "Hello, world!" << std::endl;
}
```

### What's `void`?

`void` means the function doesn't return anything. When you use `void` as the return type, you don't need a `return` statement; the function just does its job and exits.

---

## Calling Functions

Defining a function doesn't run it, you have to **call** it:

```cpp
int main() {
    getScore();
    getGrade();
    greet();
    return 0;
}
```

That's it. Define it, then call it.

---

> **Editor's Note:** C++ does not support nested functions. You cannot define a function inside another function.

> **Editor's Note:** This chapter may look rushed, but it's just an introduction. We will work with functions in later chapters!
