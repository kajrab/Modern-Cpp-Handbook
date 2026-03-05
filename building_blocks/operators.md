# Operators in C++

An operator takes one or more operands and produces a return value. Operators come in different arities; unary (one operand), binary (two operands).

---

## Arithmetic Operators

The ones you already know from math.

```cpp
int x = 10, y = 3;

x + y;   // 13
x - y;   // 7
x * y;   // 30
x / y;   // 3 (integer division, drops the decimal)
x % y;   // 1 (remainder after division, called modulo)
```

> Watch out with division. If both operands are integers, C++ does integer division and silently drops the decimal. `10 / 3` gives you `3`, not `3.33`. Use `float` or `double` if you need precision.

---

## Assignment Operators

You already know `=` but C++ has shorthand versions that combine assignment with arithmetic.

```cpp
x = 5;    // assign 5 to x
x += 3;   // same as x = x + 3
x -= 3;   // same as x = x - 3
x *= 3;   // same as x = x * 3
x /= 3;   // same as x = x / 3
x %= 3;   // same as x = x % 3
```

---

## Comparison Operators

These return either `true` or `false`.

```cpp
x == y;   // equal to
x != y;   // not equal to
x > y;    // greater than
x < y;    // less than
x >= y;   // greater than or equal to
x <= y;   // less than or equal to
```

> Do not confuse `==` with `=`. One compares, the other assigns. This is one of the most common bugs in C++.

---

## Logical Operators

Used to combine or reverse conditions.

```cpp
x > 0 && y > 0;   // AND — true only if both are true
x > 0 || y > 0;   // OR  — true if at least one is true
!(x > 0);         // NOT — flips the result
```

---

## Conditional Operator (Ternary)

A compact way to write an if-else in one line.

```cpp
int max = (x > y) ? x : y;
```

Read it as: if `x > y` is true, give me `x`; otherwise give me `y`. That is it. Useful for simple conditions but do not overuse it; nested ternaries become unreadable fast.

---

## Comma Operator

Evaluates the left expression, then the right, and returns the right.

```cpp
(++x, ++y)   // increments both x and y, returns y's new value
```

Honestly you will rarely need this one. It shows up more in `for` loops than anywhere else.

---

## Operator Precedence

C++ evaluates operators in a specific order, just like math. Multiplication and division happen before addition and subtraction. Modulo `%` has the same precedence as `*` and `/`.

```cpp
x = 4 + 11 % 3;   // 11 % 3 = 2, then 4 + 2 = 6
```

When in doubt, use parentheses. They override precedence and make your intent obvious to anyone reading the code.

```cpp
x = (4 + 11) % 3;   // now it's 15 % 3 = 0
```

Do not rely on memorizing the full precedence table. Parentheses are free.
