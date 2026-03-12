# Halts

A halt is a flow control statement that terminates the program. In C++, halts are implemented 
as functions rather than keywords, so our halt statements will be function calls.

I know we haven't properly met functions yet, but we already know the basics from the anatomy 
of a C++ program chapter, so we're fine.

---

## std::exit()

Normally your program exits when `main()` hits a `return` statement. When that happens two 
things occur in order:

- All local variables and function parameters are destroyed
- A special function called `std::exit()` is called with the return value (status code) as 
its argument

But you can call `std::exit()` yourself to terminate the program at any point:
```cpp
#include <cstdlib> // for std::exit()
#include <iostream>

int main()
{
    std::cout << "I run\n";
    std::exit(0); // terminate here, status code 0 = success

    std::cout << "I never run\n"; // unreachable
    return 0;
}
```

That's basically all it does, kills the program and hands a status code back to the OS.

> **Watch out:** `std::exit()` does not clean up local variables. If you have open network 
connections, allocated memory, or a log file that needs flushing, `std::exit()` doesn't 
handle any of that for you.

---

## std::atexit()

To handle cleanup on exit, C++ gives us `std::atexit()`. You register a function with it, 
and that function gets called automatically whenever `std::exit()` is triggered.
```cpp
#include <cstdlib>
#include <iostream>

void cleanup()
{
    std::cout << "cleaning up before exit\n";
    // close connections, flush logs, free memory, etc.
}

int main()
{
    std::atexit(cleanup); // register, don't call — no parentheses after cleanup

    std::cout << "doing stuff\n";
    std::exit(0); // cleanup() fires automatically here

    std::cout << "never reached\n";
    return 0;
}
// output:
// doing stuff
// cleaning up before exit
```

Note we pass `cleanup` not `cleanup()` - we're registering the function, not calling it right now.

> *Editor's Note:* This may feel a bit abstract since we haven't covered functions yet, but it'll click in the next chapter.

> *Editor's Note:* We'll revisit why cleanup matters once we cover pointers and memory management. For now 
just know it exists and what it's for.

---

## std::abort()

`std::abort()` terminates the program abnormally. Abnormal means something went wrong at 
runtime and the program can't recover - dividing by zero is a classic example.
```cpp
#include <cstdlib>
#include <iostream>

int main()
{
    std::cout << "something went wrong\n";
    std::abort(); // abnormal termination, no cleanup

    std::cout << "never reached\n";
    return 0;
}
```

Unlike `std::exit()`, `std::abort()` does no cleanup at all. It just stops. We'll see it 
called implicitly when we cover assertions in a later chapter.

---

## std::terminate()

`std::terminate()` is mainly used alongside exceptions, which we'll cover later. It can be 
called explicitly but more often gets called automatically when an unhandled exception slips 
through.

By default, `std::terminate()` just calls `std::abort()`.

> *Editor's Note:* Writing this chapter made me realize how connected halts are to topics we haven't covered yet. I didn't expect to have to reference this many future chapters when I planned it.
