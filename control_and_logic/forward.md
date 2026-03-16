# Forward Declarations

Welcome to one of the shortest chapters of this handbook! Today our guest is forward declarations, and do you know why it's the shortest chapter? Because it's so easy to understand!

```cpp
int main(){
    sum(3, 5);
    return 0;
}

int sum(int x, int y) { return x + y; }
```

Do you think it's going to work? NO!

But why though?

Because you did not define the function yet... But wait, did you define it? Then why still can it not be used?

Because you defined it *after* the main function, and that's a no-no in C++! Main runs first and it tries to access the `sum` function, but it sees it's not defined yet, and ta-da, error!

But a fix is available and it's easy:

```cpp
int sum(int x, int y);

int main(){
    sum(3, 5);
    return 0;
}

int sum(int x, int y) { return x + y; }
```

A forward declaration! It's like you declare a function before defining it, yes, it's not defining! Do not mix the words up! A definition is when you write out your full function (parameters and body). A declaration just tells C++ that this function exists and where to find it before main runs.

It's useful because programmers can see all declared functions early, and it makes the code much more readable, especially when you put main first.

## Declaration vs. Definition, Don't Mix Them Up

Since we just touched on this, let's make it stick:

| Term | What it means | Ends with |
|---|---|---|
| **Declaration** | Tells the compiler the function's name, return type, and parameters | `;` |
| **Definition** | The full function, declaration + body | `}` |

Every definition is also a declaration, but not the other way around. A forward declaration is *just* a declaration, no body, just the signature and a semicolon.

## Where Forward Declarations Really Matter: Header Files

In small programs, rearranging function order works fine. But in real projects, your code is split across multiple `.cpp` files, and that's where forward declarations become essential.

Say `main.cpp` wants to use `sum` from `math.cpp`. It can't see that file at all. So you put the declaration in a **header file**:

```cpp
// math.h
int sum(int x, int y);
```

```cpp
// math.cpp
#include "math.h"

int sum(int x, int y) { return x + y; }
```

```cpp
// main.cpp
#include "math.h"

int main(){
    sum(3, 5);
    return 0;
}
```

Now `main.cpp` knows `sum` exists without needing to see its definition. That's forward declarations doing real work.

> *Editor's Note:* We are going to cover this concept in more detail later!

See ya, that's all for this chapter.
