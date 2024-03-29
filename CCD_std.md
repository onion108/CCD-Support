# Unsupported Syntax

## Statements

C Code Develop seems not to support expression as a statement. i.e., the following code won't compile on C Code Develop:
```c
int main(void) {
    int x, y;
    5;
    x = 3, y = 6;
}
```

As a work-around, you can add parenthesis around the expression to make it valid for C Code Develop:
```c
int main(void) {
    int x, y;
    (5);
    (x = 3, y = 6);
}
```

C statements that are considered «valid» by C Code Develop are listed as following (tested, may not be complete):
```c
// A function call.
my_function(arg1, arg2, arg3);

// A single assignment.
my_var = 5;
my_struct.my_member = "Hello World! ";
my_var += 1;

// Expression inside parenthesis.
(1 + 1);

// Variable declaration.
int a;
const char *a, *b;

// A single increment/decrement of a variable.
a++;
a--;
```

## Expressions

### [Compound Literals](https://en.cppreference.com/w/c/language/compound_literal)

C Code Develop doesn't support Compound Literals. i.e., the following code won't compile:
```c

#include <stdio.h>

struct Something {
    int a;
};

int main(void) {
    const float *pc = (const float []){1e0, 1e1, 1e2};
    struct Something sth = { .a = 3 };
}

```

## Pointer Types

### Function Pointer
C Code Develop currently partially supports function pointer types. However, function pointer types cannot be used in function parameters directly, instead a `typedef` is required to wrap the function pointer type due to C Code Develop interpreter's internal implementation.

### Pointer To Arrays
C Code Develop doesn't support this. thus, this code won't compile:
```c

int main(void) {
    int a[2];
	int (*ap)[2] = &a;
}

```

## Macros

### Macros with Parameters
C Code Develop doesn't support them well. It seems to treat macros with parameters as ordinary function, hence this code

```c
#include <stdio.h>
#define SQUARE(X) X * X

int main(void) {
    int a = SQUARE(2+3);
    printf("%d\n", a);
}

```

prints 25, instead of 11.

There are also several weird behaviors when using function-like macros. See [wr00](CCD_weird_results.md#wr00)


# Extended Syntax

## C++ extension

### References

References are supported by C Code Develop.

### `using namespace std;` and `cin`/`cout` in Header `<iostream>`
These features are built into the C Code Develop interpreter.

## `AutoTree` extensions (Documentation: [Chinese](https://docs.forgetive.org/cdenvc/autotree.h/__article__))

### Built-in Type `AutoTree`
This type represents a reference count managed tree. C Code Develop supports a bunch of funtions to operate `AutoTree`s, including serialization/deserialization with JSON, reference counter management etc.

### `AutoTree` Literals
C Code Develop introduced a new literal syntax to create `AutoTree` instances more convenient.
It's a JSON-like syntax with `@` prefix.

Preview:
```objc
AutoTree tree = @{
  a: v+2*2,
  b: 1,
  c: ["main", {
    f: 1
  }],
  d: {
    e: 2
  }
};
```

Especially, C Code Develop introduced more syntax for `AutoTree` literals to make it work better with C Code Develop's built-in UI library, CCDUI. Documentation [here (Chinese)](https://docs.forgetive.org/cdenvc/ccduicomp.h/__article__).

