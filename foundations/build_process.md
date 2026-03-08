# How C++ Builds Work

A compiler is actually a simple tool at its core. It reads your code, checks if it follows C++ rules, and if something is wrong; it throws an error and stops. 

Once your code passes, the compiler translates it into an **object file**  your C++ code converted into machine language instructions.

---

## The Linker

Compiler succeeded? Nice. Now another program called the **linker** enters the game.

The linker takes all your object files and combines them into the final output. A few things it handles:

**Connects your files together** — if you define something in one `.cpp` file and use it in another, the linker is what connects the two. If it can't find the connection, you get a linker error and the process aborts.

**Links libraries** — it pulls in any external libraries your project depends on.

**Produces the output** — usually an executable you can run, or a library file if that's how your project is set up.

So the full picture looks like this:

```
Object Files + C++ STL + Other Libs → Linker → Executable
```

---

## The Standard Library

C++ ships with a massive built-in library called the **C++ Standard Library** — or just "the standard library." It's a collection of prebuilt functionality so you don't have to reinvent the wheel every time.

The most common part you'll use early on is **iostream** handles printing to the console and reading keyboard input. Almost every C++ program uses it in some way.

Good news: most linkers automatically link the standard library by default. You don't need to do anything special.

---

## Third Party Libraries

Sometimes the standard library doesn't have what you need. Say you want to play audio in your program ,C++ has nothing built-in for that. You could write it yourself from scratch, handle file reading, OS audio routing, hardware output... or you could just grab a library that already does all of that.

That's what third party libraries are. Built by external teams, not part of the C++ standard, but plug right into your project.

---

## Building

Since there are multiple steps involved — compiling, linking, output — the whole process is called **building**. The final result is called a **build**.

For bigger projects, people use build automation tools like `make` to handle all of this automatically instead of running every step manually.
