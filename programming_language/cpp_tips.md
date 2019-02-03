# Cpp Tips

# 1. Dynamic Memory Allocation(动态内存分配)
## 1.1. Not Free Allocated Memory Case
* Not delete after allocate by `new`.
* Raise error before running `delete`.

for instance:
```cpp
ObjectType* temp_ptr = new ObjectType();
temp_ptr->foo();
delete temp_ptr;
```
If not calling `delete` or raising error at `temp_ptr->foo();`, 
the memory allocated by `new` will not free, which will cause 
certain block in memory space call not be allocate by other codes.


# 2. Smart Pointer(智能指针)


# 3. Class, Function, Variable
## 3.1. Variable
### 3.1.1. Notions and Syntax Details
* **Static Variable and `static`** 
* **`const`**  
Refer to https://www.cnblogs.com/Forever-Kenlen-Ja/p/3776991.html.
    * using `const` decorate function/method's arguments.   
    Sometimes this is not necessray, since in certain cases, the 
    functions will build arguments' copy in function body. But in 
    some other cases, such as the arguments include pointer, the 
    `const` before these pointer arguments can protect the value 
    pointed by these pointer modified by function. 
    For some self-defined type arguments, copying these arguments 
    in function body is low efficiency, so we can use pointer of 
    these variables with a `const` decoration for protection.   
    For instance:
    ```cpp
    void StringCopy(char* strDestination, const char *strSource);
    ```
    Using `const` decorate `char *strSource` can protect the value
    pointed by `strSource` from modified by function.
    * using `const` decorate function/method's return(const修饰函数的返回值)

    * using `const` decorate function/method itself(const放在函数体前)  
    For instance:
    ```cpp
    int add(int a, int b) const {
        return a + b;
    };
    // It error if use `a = 3;` before `return a + b;`.
    ```
    In this case, in function body(函数体), we can not modify any 
    variables.
* **`constexpr`**  
    Represents "constant expression(常量表达式)", which value will 
    never changed and calculated during compiling phase, 
    for instance:
    ```cpp
    const int i = 3; // Also a constant expression.
    const int j = i + 1; // Also a constant expression.

    int f(int a) {
        return (a + 1);
    }
    // This is not constant expression, since the value of 
    // `m` can only gotten during running phase. 
    const int m = f(1); 
    // So, we can also coding as:
    constexpr int i = 3;
    constexpr int j = i + 1;

    // we can not write `constexpr int m = f(1)` since `f` 
    // is not a "constexpr function".
    ```
    Refer to https://www.cnblogs.com/td15980891505/p/5137013.html.
 
    * **constexpr function(编译期函数)**
    For constexpr function, using `constexpr` before function 
    declaration. Here we have some new notions, such as 
    **compiling phase constant**, etc. For instance:
    ```cpp
    // `array_size` is a "compiling phase constant".
    constexpr auto array_size = 10;
    // So the following code could be right compiled, since 
    // the compiler can get the value of `array_size` during 
    // compiling phase.
    std::array<int, array_size> data2; 

    // The following case con not be compiled, since the compiler 
    // con not get the value of value of `array_size` during 
    // compiling phase so can not compile next line.
    const auto array_size = sz; 
    std::array<int, array_size> data;  
    ```
    Now extending to constexpr function:
    ```cpp
    // cpp 11
    constexpr int factorial(int n) {
        return n == 0 ? 1 : n * factorial(n - 1);
    }
    // cpp 14
    constexpr int factorial2(int n) {
        int result = 1;
        for (int i = 1; i <= n; ++i) {
            result *= i;
        }
        return result;
    }
    ```
    Getting the value of expression is during compiling phase is 
    pretty useful. In cpp 11, there are some limitations, such as you 
    can not define declare variables in constexpr function body, 
    can not using "for loop",  can only has a `return` expression 
    in function body, stc. This means we always have to use 
    "iteration function(递归函数)" form many times.  
    In cpp 14, many of these limitations has been droped.  
    Refer to https://blog.csdn.net/zwvista/article/details/54429416.
   

## 3.2. Function

## 3.3. Class
### 3.3.1. Syntax Details
* `explicit`  
Keyword `explicit` can only used for decorating constructor function 
with only one non-default argument.  
Refer to https://blog.csdn.net/qq_37233607/article/details/79051075.


# 4. Code Reuse(代码重用)
## 4.1. Macro(宏)
### 4.1.1. Syntax Details 
- **`##` and `#`**: `##` used for linking arguments, `#` used for 
replacement or, "converting to string", refer to following example:

```cpp
#define CONVERT(name) #name
int main() {
    printf("You and %s are friends.\n", CONVERT(James));
    return 0;
};
// This will print "You and James are friends.".
```
```cpp
#define CAT(batman, robin) batman ## robin
int main() {
    printf("%s\n", CAT(A, BCD));
    return 0;
}
// This will print "ABCD".
```
- **`##__VA_ARGS__` and `__VA_ARGS__` and `...`**: `__VA_ARGS__` and 
`...` are similiar, both means the number of macro function's 
arguments is variable; `##__VA_ARGS__` will be helpful to handling 
the case that variable arguments number is zero. Refer to 
https://blog.csdn.net/guozhongwei1/article/details/82659435.



