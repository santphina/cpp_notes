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



