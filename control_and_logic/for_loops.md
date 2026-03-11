# For Loops

A `for` loop runs a block of code a set number of times. It's the go-to loop when you know exactly how many iterations you need.

---

## Syntax

```cpp
for (initialization; condition; update) {
    // body
}
```

All three parts live in the loop header, which keeps everything in one place and makes it easy to read at a glance.

```cpp
for (int i = 0; i < 5; i++) {
    std::cout << i << ' ';
}
// output: 0 1 2 3 4
```

Think of it like this:

- `int i = 0` - start here
- `i < 5` - keep going as long as this is true
- `i++` - do this after each iteration

---

## Infinite for loops

Leave all three parts empty and the loop runs forever.

```cpp
for (;;) {
    // runs indefinitely
}
```

This is equivalent to `while (true)`. You'll see this pattern in game loops and event loops where you want to keep running until something explicitly breaks out.

```cpp
for (;;) {
    std::cout << "Running...\n";
    if (someCondition) break;   // only way out
}
```

> *Editor's Note:* Personally I prefer `for (;;)` for infinite loops, but that's just a personal preference. To be fair, `while (true)` is easier to read, so relying on it could improve teamwork; it's more approachable at a glance.

---

## Nested for loops

A loop inside a loop. The inner loop completes all its iterations for every single iteration of the outer loop.

```cpp
for (int i = 0; i < 3; ++i) {
    std::cout << '\n';
    for (int j = 0; j < 3; ++j) {
        std::cout << '+' << ' ';
    }
    std::cout << '\n';
}
// output:
// + + +
// + + +
// + + +
```

A classic use case is working with grids, the outer loop handles rows, the inner loop handles columns.

Keep in mind that `break` and `continue` only affect the nearest enclosing loop, not all of them.

---

## Range-based for loops

A cleaner syntax for iterating over a collection from start to finish. Instead of managing an index manually, you just say "give me each element."

```cpp
for (type variable : collection) {
    // body
}
```

```cpp
std::vector<int> nums = {1, 2, 3, 4, 5};

for (int n : nums) {
    std::cout << n << ' ';
}
// output: 1 2 3 4 5
```

Here, `n` takes each value in `nums` one by one. Think of it like:

- `n` becomes 1 - first element of the collection
- Do whatever is in the body with it
- Loop starts again and now `n` becomes 2 - second element
- And so on until the collection runs out

### With arrays

Arrays are collections that store multiple values of the same type. They'll be covered in detail later - for now just know that a range-based for loop works on them the same way.

```cpp
int nums[] = {10, 20, 30, 40, 50};

for (int n : nums) {
    std::cout << n << ' ';
}
// output: 10 20 30 40 50
```
