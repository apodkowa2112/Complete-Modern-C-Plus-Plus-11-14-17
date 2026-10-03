# Templates
```cpp
template <typename T> T Max( T x, T y) { return x > y ? x : y; }
```
* No difference between `template <typename T>` and `template <class T>`.
## Template argument deduction
* Process of deducing the types
* Each type is deduced from the argument
* No type conversions performed
* After deduction, template is instantiated
* Deduction can be overridded using this syntax: `Max<int>(3, 5);`
* Templates should always be implemented in the header file.
* Templates always assume the first argument as the type, so `Max(3, 5.5)` won't work with a single `typename T` defined.
* This can be overridden with the syntax `Max<double>(3, 5.5)`
* Function pointer syntax: `int (*pfn)(int, int) = Max;`

## Explicit Specialization
* Motivation: `Max<char *>()` compares address locations, not values.
* Template specialized for a particular type
* Optimal implementation for a particular type (in cpp file).
```cpp
template<> const char * Max(const char* x, const char* y) {
    return strcmp(x,y) > 0 ? x : y;
}
```

## Non-type template arguments
```cpp
tempate<int size> void Print() { cout << size << endl; } // Print<3>();
```
* Non-type template arguments must be `constexpr`s (addresses, refs, integers, nullptr, enums).
* Use case: Passing size arguments for C-arrays:
```cpp
template<typename T, int size>
T Sum( T (&arr)[size] ) { // Calling syntax: Sum(arr); The size argument is implicit!
    T sum{};
    for (int i = 0; i < size; ++i) {
        sum += arr[i];
    }
    return sum;
}
```

## Perfect Forwarding
* Motivation: Requiring constructors that process any combination of r-value/l-value refs (2^nMember possibilities).
* std::forward can be used to preserve caller's r-value/l-value references.

## variadic functions
* Multiple numbers of arguments (i.e. printf);
```cpp
template <typename T> 
void Print(std::initializer_list<T> args) {
    for (const auto &x : args) {
        std::cout << x << " ";
    }
}
```
* Problem: all args must be same type.
* Solution:
```cpp
//Template parameter pack
template<typename T, typename...Params>
//Function parameter pack
void Print(T t, Params... args) {
    Print(args...);
}
template<typename T> Print(T t) {
    std::cout << t << " ";
}
```

## Class Templates
This class is restrictive:
```cpp
class Stack {
    int m_Buffer[512];
    int m_Top{-1};
public:
    void Push(int elem) { m_Buffer[++m_Top] = elem; }

    int Pop()       { return m_Buffer[m_Top--]; }
    int Top() const { return m_Buffer[m_Top]; }
    bool IsEmpty()  { return m_Top < 0; }
}
```
Do this instead:
```cpp
template<typename T, int size>
class Stack {
    T m_Buffer[size];
    int m_Top{-1};
public:
    Stack() = default;
    Stack(const Stack& obj) {
        m_Top = obj.m_Top;
        for (int i = 0; i <= m_Top; ++i) {
            m_Buffer[i] = obj.m_Buffer[i];
        }
    }
    void Push(const T& elem) { m_Buffer[++m_Top] = elem; }
    T Pop();
    const T& Top() const { return m_Buffer[m_Top]; }
    bool IsEmpty()  { return m_Top < 0; }
    static Stack Create(); // Shorthand `Stack` only works in class definition
}
template<typename T, int size>
T Stack<T, size>::Pop() { return m_Buffer[m_Top--]; }
```

## Type Traits
* Compile-time characteristics
* Transform type properties
* Type Trait options:
    * is_void:           if a type is void
    * is_integral:       if a type is integral type (Refs don't count)
    * is_floating_point: if a type is floating-point (Refs don't count)
    * is_array:          if a type is an array
    * is_enum:           if a type is an enumeration
    * is_union:          if a type is a union
    * is_class:          if a type is a non-union class
    * is_function:       if a type is a function
    * is_pointer:        if a type is a pointer
    * is_null_pointer:   (C++14) if a type is `std::nullptr_t`
           
```cpp
#include <type_traits>
template<typename T>
T Divide(T num, T den) {
    if (std::is_floating_point<T>::value == false) {
        std::cerr << "Only floating point types supported" << endl;
        return 0;
    }
    return a / b;
}
```
## `static_assert`
* Tests an expression during compile time.
* Arguments: expression and user defined message.
* If false, compiler displays message and compilation fails.
* Use case: Prevent compilation for incompatible architectures:
```cpp
static_assert(sizeof(void*)==4, "32-bit supported only");
```
