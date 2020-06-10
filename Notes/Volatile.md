## Volatile

Quoting from the C++ Standard ($7.1.5.1/8)

> [..] volatile is a hint to the implementation to **avoid aggressive optimization involving the object** because the value of the object might be changed by means undetectable by an implementation.[...]

**Example**

```
int main (){
   int value;
   value++;
}
int main (){
   volatile int value;
   value++;
}
```

There are two blocks of code. In the first block the volatile keyword is not present. So for the first case, the variable will be copied from memory to CPU register, then the operations are performed. In the second case the volatile is present. So in this case the variable will not be copied from memory to registers.



c++编译器会对程序进行非常大程度的优化，例如未定义行为就是这样变成bug的。程序的运行会极大得受到IO的影响，Volatile关键字就是告诉编译器不要做优化，按照程序的定义来。 



```c++
Volatile bool m_bWorking;
//Better to be:
boost::atomic<bool> m_bWorking;
```



