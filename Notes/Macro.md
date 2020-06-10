# Macro

Macros are categorized into two main groups: object-like macros and function-like macros. Macros are treated as a token substitution early in the compilation process. This means that large (or repeating) sections of code can be abstracted into a preprocessor macro.

```c++
// This is an object-like macro
#define    PI         3.14159265358979

// This is a function-like macro.
// Note that we can use previously defined macros
// in other macro definitions (object-like or function-like)
// But watch out, its quite useful if you know what you're doing, but the
// Compiler doesnt know which type to handle, so using inline functions instead
// is quite recommended (But e.g. for Minimum/Maximum functions it is quite useful)
#define    AREA(r)    (PI*(r)*(r))

// They can be used like this:
double pi_macro   = PI;
double area_macro = AREA(4.6);
```



**Function Implementation vs. Macro Implementation **

```cpp
//Function Implementation  
char ToLower(char c) {
    return static_cast<char>(c + 32);
}

//Macro Implementation  
#define ToLowerM(c) static_cast<char>(c + 32)

#include <iostream>
int main() {
    std::cout << ToLowerM('A');
    /**
    * To the compiler, it is equivalent to: std::cout << static_cast<char>('A' + 32);
    * 相当于copy和paste，所以宏实现是没有物理地址的
	**/
}
```

