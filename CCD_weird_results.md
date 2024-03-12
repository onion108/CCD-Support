# Weird Results in C Code Develop

## wr00

This code:
```c
#include <stdio.h>
#define SQUARE(X) X * X

int main(void) {
    printf("%d\n", SQUARE(2+3));
}
```
prints 0, while
```c
#include <stdio.h>
#define SQUARE(X) X * X

int main(void) {
    int a = SQUARE(2+3);
    printf("%d\n", a);
}
```
prints 25.

