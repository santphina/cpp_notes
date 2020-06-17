# Thread Undefined Behavior

A Thread must reach one of the following four status in order to not to be an undefined behavior:

1. 正常结束，e.g.如果有死循环的情况下，加log会影响程序的性质
2. 存取volatile
3. 同步
4. IO操作

# Functions

## tolower

Convert uppercase letter to lowercase. The corresponding header file: <cctype>

```c++
int tolower ( int c );
```

The behavior is undefined, if the input parameter is neither an unsigned char nor EOF. For example,

```c++
std::transform(str.begin, str.end(),str.begin(),tolower)
```

# Floating Points

浮点数，例如double，不能和int比较，也不能和别的浮点数直接比较，因为浮点数并不精确。未定义行为举例：

```c++
//Undefined Behaviors
double tc = 0.0;
if(tc == 0);
if(tc == 0.0)
```

# Uninitialized Variables & Constants

都会给予存储空间。const不初始化的话就不分配存储空间。 variable不初始化，compiler就会随便赋值

```c++
int main() {
  //const int buf;       // Error: must be initialized
  int cnt = 0;         // OK
  const int sz = cnt;  // OK
  ++cnt;  // OK
  //++sz;   // Error: cannot change the value of a const variable

  return 0;
}
```

```c++
#include <iostream>

int main() {
  { //(a)
    //int i = -1, &r = 0;  // Error: a nonconst reference cannot be initialized to a literal
  }
  { //(b)
    int i2;
    int *const p2 = &i2;  // OK
  }
  { //(c)
    const int i = -1, &r = 0;  // OK
  }
  { //(d)
    int i2;
    const int *const p3 = &i2;  // OK
  }
  { //(e)
    int i2;
    const int *p1 = &i2;  // OK
  }
  { //(f)
    //const int &const r3;  // Error: 1. there is not top-level const for reference
                            //        2. a const reference must be initialized when defined
  }
  { //(g)
    int i;
    const int i2 = i, &r = i;  // OK, with a warning of using undefined variable `i`
    //r = 5;  // Error: cannot change the value of `i` through `r`
    std::cout << i << " " << i2 << " " << r << std::endl;  // Undefined Undefined Undefined Undefined
    i = 5;    // But the value can be changed directly
    std::cout << i << " " << i2 << " " << r << std::endl;  // 5  Undefined 5
    i = 10;   // And when visit through `r`, the new value is returned
    std::cout << i << " " << i2 << " " << r << std::endl;  // 10 Undefined 10
  }

  return 0;
}
```

```c++
#include <iostream>

int main() {
  //(a)
  //int i, *const cp;  // Error: a const pointer must be initialized
  //(b)
  //int *p1, *const p2;  // Error: a const pointer must be initialized
  //(c)
  //const int ic, &r = ic;  // Error: const int `ic` must be initialized
  //(d)
  //const int *const p3;  // Error: a const pointer must be initialized
  //(e)
  const int *p;  // OK

  return 0;
}
```

```c++
int main() {
  int i, *const cp = &i;
  int *p1, *const p2 = p1;
  const int ic = 5, &r = ic;
  const int *const p3 = &ic;
  const int *p;

  i = ic;  // OK
  p1 = p3;  // Error: low-level const doesn't match
  p1 = &ic;  // Error: low-level const doesn't match
  p3 = &ic;  // Error: cannot assign value to a const variable
  p2 = p1;  // Error: cannot assign value to a const variable
  ic = *p3;  // Error: cannot assign value to a const variable

  return 0;
}
```



