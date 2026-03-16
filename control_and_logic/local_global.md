# Local and Global Scope

Previous chapter we talked about parameters and how they are only available for the function they're declared in. Now we're gonna broaden this topic, our new subject is global and local scope.

It's a new name for something you already know, but let me define it one more time:

```cpp
// global scope
void greet(){
  // local scope
}
int main(){
  // local scope
}
```

Inside a function or a block (such as switch-case or loops) is **local scope**, and outside any block is **global scope**. The key difference: variables defined in global scope are accessible everywhere. Local scope variables? Strictly local, you can't use them outside.

```cpp
int main(){
  while(true){
    int x = 10;
  }
  // x is not defined here, it died when the loop ended
  std::cout << x << '\n';
}
```

```cpp
int sum_it_up(int x, int y){
  return x + y;
} // x and y destroyed after return
```

Think of `return` as a destructor. Whenever execution jumps out of a scope, everything born inside it gets destroyed.

---

## Out of scope vs Going out of scope

These two sound similar but they mean different things.

**Out of scope** means a variable simply doesn't exist in the current context. You're trying to use something that was never declared where you're standing.

```cpp
int main(){
  {
    int x = 5;
  }
  std::cout << x; // x is out of scope, it was never declared here
}
```

**Going out of scope** is the process, the moment execution leaves the block where a variable was born. That's when its lifetime ends and it gets destroyed.

```cpp
int main(){
  {
    int x = 5;
  } // x is going out of scope right here, at this closing brace
}
```

So "out of scope" is a state (it's inaccessible), and "going out of scope" is the event (it's dying). They're related but not the same thing.

---

## Function Parameters vs Local Variables

Both live in local scope, but they have slightly different origins.

A **local variable** is something you declare inside the function body yourself:

```cpp
void greet(){
  std::string message = "hello"; // local variable
}
```

A **function parameter** is declared in the function signature and gets its value from the caller:

```cpp
void greet(std::string name){ // name is a parameter
  std::string message = "hello " + name; // message is a local variable
}
```

In terms of lifetime, they behave the same. Both are destroyed when the function returns. The difference is just where they come from: parameters arrive from outside, local variables are born inside.

> *Editor's Note:* parameters are essentially local variables with a pre-assigned value. Under the hood, the compiler treats them almost identically once you're inside the function body.

---

## Introduction to Temporary Objects

Sometimes in C++, objects are created that you never explicitly named. These are called **temporary objects** (also known as rvalues, but we'll get to that later).

```cpp
std::cout << std::string("hello") << '\n';
```

That `std::string("hello")` is a temporary. You constructed it, used it in the expression, and it's gone by the end of the statement. You never gave it a name, never stored it. It existed just long enough to be useful.

Another example:

```cpp
int add(int x, int y){ return x + y; }

int main(){
  std::cout << add(3, 4) << '\n'; // the result 7 is a temporary
}
```

The `7` returned from `add` is a temporary integer. It gets passed to `cout`, then immediately discarded.

Temporaries are destroyed at the end of the **full expression** they appear in, which is usually the semicolon. This is called temporary lifetime, and it matters more once you start working with references.

```cpp
const int& ref = add(3, 4); // binding a const ref extends the temporary's lifetime
```

We'll dig into that last part properly when we cover references. For now just know: temporaries exist, they're short-lived, and C++ is very deliberate about when they die.
