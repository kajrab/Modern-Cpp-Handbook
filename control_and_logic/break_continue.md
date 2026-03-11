# Break and Continue

Both `break` and `continue` are jump statements, they alter the normal flow of a loop (or a `switch`) without needing a condition baked into the loop header itself.

---

## break

`break` exits the nearest enclosing loop or `switch` block immediately. The rest of the loop body is skipped, and execution resumes after the closing brace.

```cpp
for (int i = 0; i < 10; ++i) {
    if (i == 5) break;   // stop as soon as i hits 5
    std::cout << i << ' ';
}
// output: 0 1 2 3 4
```

"Nearest enclosing" matters in nested loops, `break` only escapes one level.

```cpp
for (int i = 0; i < 3; ++i) {
    for (int j = 0; j < 3; ++j) {
        if (j == 1) break;   // exits inner loop only
        std::cout << i << ',' << j << ' ';
    }
}
// output: 0,0  1,0  2,0
```

> *Editor's Note:* To break out of multiple levels, common patterns are using a flag variable, restructuring into a function and using return, or using goto; the only option that's genuinely efficient for this case.

---

## continue

`continue` skips the rest of the current loop iteration and jumps to the next one. The loop itself keeps running.

```cpp
for (int i = 0; i < 6; ++i) {
    if (i % 2 == 0) continue;   // skip even numbers
    std::cout << i << ' ';
}
// output: 1 3 5
```

In a `while` or `do-while` loop (will be covered in the next chapter), `continue` jumps to the condition check. Make sure your loop variable still updates, or you'll get an infinite loop.

```cpp
int i = 0;
while (i < 6) {
    ++i;                         // increment BEFORE continue, or loop never ends
    if (i % 2 == 0) continue;
    std::cout << i << ' ';
}
// output: 1 3 5
```

---

## In a range-based for loop

Both work exactly as expected, the loop variable advances automatically, so there's no foot-gun with `continue` here.

> *Editor's Note:* I'll cover range-based for loops later. In short, they're loops that iterate over a range; say you have an array with 5 elements, the loop runs 5 times because the range is 5. I also noticed I haven't written a part for arrays yet, so for now just think of them as collections that store data. I'll keep updating this as I go.

```cpp
std::vector<int> nums = {1, 2, 3, 4, 5};

for (int n : nums) {
    if (n == 3) continue;   // skip 3
    std::cout << n << ' ';
}
// output: 1 2 4 5
```

Here, `n` takes the values 1, 2, 3, 4, and 5 in order. Think of it like:
- `n` becomes 1 - first element of the array
- Check if it's 3 or not (if it is, skip it; if not, print it)
- Loop starts again and now `n` becomes 2 - second element of the array

---

## In a switch statement

`break` is what terminates a `case` in a `switch`. Without it, execution falls through to the next case.

```cpp
int x = 2;

switch (x) {
    case 1:
        std::cout << "one";
        break;
    case 2:
        std::cout << "two";
        break;   // without this, "three" would also print
    case 3:
        std::cout << "three";
        break;
    default:
        std::cout << "other";
}
// output: two
```

Intentional fallthrough is valid but should be marked with `[[fallthrough]]` to signal it's deliberate, not a bug.

```cpp
switch (x) {
    case 1:
    case 2:
        std::cout << "one or two";   // implicit fallthrough from case 1 to case 2
        break;
    default:
        break;
}
```

```cpp
switch (x) {
    case 1:
        doSomething();
        [[fallthrough]];   // explicit: yes, this is intentional
    case 2:
        doSomethingElse();
        break;
}
```

You've already covered this, but it's worth mentioning again to reinforce it.

---

## Quick reference

| Statement  | Works in          | Effect                                      |
|------------|-------------------|---------------------------------------------|
| `break`    | loops, `switch`   | exits the nearest enclosing block           |
| `continue` | loops only        | skips to the next iteration                 |
| `[[fallthrough]]` | `switch` only | marks intentional case fallthrough    |
