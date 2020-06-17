# Pointer and Reference

A pointer is an object whose value is the address of another object.

A reference is not an object. It is an alias of another object.

```c++
#include <iostream>

int main() {
  int i;
  int *ip = &i;

  std::cout<< "i = " << i << std::endl;
  std::cout<< "ip = " << ip << std::endl;
  std::cout<< "&i = " << &i << std::endl;

  *ip = 10;
  std::cout << i << " " << *ip << std::endl;  // 10 10
  i = 5;
  std::cout << i << " " << *ip << std::endl;  // 5 5

  return 0;
}
```



`if (p)` means if the pointer `p` is not null.

`if (*p)` means if the object pointed by the pointer is not false (which means the object is not null or zero etc.).



**Given a pointer p, can you determine whether p points to a valid object?**

No, you can't. Why? Because it would be expensive to maintain meta data about what constitutes a valid pointer and what doesn't, and in C++ you don't pay for what you don't want.

And you don't *want* to check whether a pointer is valid, because you *know* where a pointer comes from, either because it's a private part of your code that you control, or because you specified it in your external-facing contracts.