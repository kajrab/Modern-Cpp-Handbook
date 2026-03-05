# Variables in C++

I really wanted to start this handbook with variables because they are easier to learn and it's actually a concept we have known for years thanks to math classes.

I assume everyone here knows what a variable is but let's define it one more time for the sake of the handbook.

Variables are things that keep values. They can be changed over time because their value is assigned by the user, the programmer, or whoever is working with them.

In C++, variables are not so different from math; you create a variable and it contains a value that you assigned.

> Variables are stored in RAM (Random Access Memory). Once you exit the program, your variables are cleared from RAM.

```cpp
int integer_var = 15;
float decimal_var = 15.0;
char character_var = 'a';
long long_integer_var;        // can store larger integers than int
bool condition_var = true;    // stores true or false
double long_float_var;        // 64-bit decimal, more precise than float
long long longest_var;        // for the largest integer values
```

---

## Data Type Sizes

| Type | Size | Range |
|---|---|---|
| `bool` | 1 byte | true / false |
| `char` | 1 byte | -128 to 127 |
| `int` | 4 bytes | -2,147,483,648 to 2,147,483,647 |
| `long` | 4 or 8 bytes | platform dependent |
| `long long` | 8 bytes | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| `float` | 4 bytes | ~6-7 decimal digits of precision |
| `double` | 8 bytes | ~15-16 decimal digits of precision |
| `long double` | 8, 12, or 16 bytes | platform dependent, higher precision than double |

As you can see, variables store values so we can use them later in the program without writing them again and again.

We also have a data type called `string` but that comes from the Standard Library; we'll cover it later. Same goes for non-primitive types like objects and compound types. Once those sections are ready, they'll be linked here.

---

## Variable Declaration

Declaring a variable means telling C++ it exists and what type it is.

Syntax: `data_type variable_name;`

```cpp
float version;   // declare a variable of type float
version = 5.0;     // assign the value 5 to it
```

---

## Variable Initialization

Initialization means declaring and assigning a value at the same time. There are 5 ways to do this — 3 classic, 2 modern. Since this is a modern C++ handbook, we prefer the modern ways, but knowing all of them is useful.

```cpp
int num;                      // default-initialization (no value assigned)

// Traditional:
int second_num = 5;           // copy-initialization
float pi_number (3.14);       // direct-initialization

// Modern:
char character_var { 'a' };   // direct-list-initialization
bool is_positive {};          // value-initialization (defaults to 0 / false)
```

**Why prefer modern initialization?**

Direct-list-initialization with braces `{}` is safer. It does not allow narrowing conversions; meaning if you accidentally try to store a `double` inside an `int`, it will throw a compile error instead of silently losing data. The traditional ways would just let it happen without warning.

```cpp
int x = 3.14;    // compiles fine, silently drops the decimal; x becomes 3
int y { 3.14 };  // compile error, C++ catches the mistake for you
```

That alone is a good reason to use braces by default.

---

## Initializing Multiple Variables

You can declare and initialize multiple variables of the same type in one line.

```cpp
bool f, t;                 // declare f and t, not initialized
bool f { false }, t { true };  // declare and initialize both

int a = 5, b = 6;          // copy-initialization
int c ( 7 ), d ( 8 );      // direct-initialization
int e { 9 }, f { 10 };     // direct-list-initialization
int i {}, j {};            // value-initialization
```

---

## [[maybe_unused]]

Sometimes you declare a variable but do not end up using it. C++ compilers will warn you about this; unused variables are usually a sign of a mistake or leftover code.

If you intentionally want to keep an unused variable without seeing the warning, you can mark it with `[[maybe_unused]]`:

```cpp
[[maybe_unused]] int debug_mode = 1;
```

This tells the compiler "I know it's unused, it's intentional, stop warning me." Useful during development when you're building things incrementally and some variables are placeholders for now.
