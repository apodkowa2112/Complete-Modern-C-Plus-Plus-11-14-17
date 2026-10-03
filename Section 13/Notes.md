# Lambda Expressions
Old:
```cpp
template <typename T, int size>
void Sort(T (&arr)[size]) {
    for (int i = 0; i < size-1; ++i) {
        for (int j = 0; j < size-1; ++j) {
            if ( arr[j] > arr[j+1] ) {
                T temp     = std::move( arr[j]     );
                arr[j]     = std::move( arr[j + 1] );
                arr[j + 1] = std::move( temp       );
            }
        }
    }
}
```
Problems:
* Ascending only
* Doesn't work for C-strings
```cpp
using Comparator = bool(*) (int, int);
template <typename T, int size>
void Sort(T (&arr)[size]), Comparator comp ) {
    for (int i = 0; i < size-1; ++i) {
        for (int j = 0; j < size-1; ++j) {
            if ( comp (arr[j], arr[j+1]) ) {
                T temp     = std::move( arr[j]     );
                arr[j]     = std::move( arr[j + 1] );
                arr[j + 1] = std::move( temp       );
            }
        }
    }
}
```
Problem:
* Comparator specialized for `int`s.
Solution:
```cpp
template <typename T, int size, Comparator>
void Sort(T (&arr)[size]), Comparator comp ) {
    for (int i = 0; i < size-1; ++i) {
        for (int j = 0; j < size-1; ++j) {
            if ( comp (arr[j], arr[j+1]) ) {
                T temp     = std::move( arr[j]     );
                arr[j]     = std::move( arr[j + 1] );
                arr[j + 1] = std::move( temp       );
            }
        }
    }
}
```

It can be useful for `Comparator` to be a functor/function object:
* Object with overloaded call operator: `operator()`
* Usually implemented as structs

Function Object Tradeoffs:
* specified at compile time -> easy to optimize
* static in nature
* Can store state

Function Pointer Tradeoffs:
* Can be specified at runtime
* Dynamic in nature --> difficult to optimize
* invoked through a pointer

## Lambda expressions:
* Anonymous function object
* Implemented as a nameless function object.
```cpp
    [/*lambda introducer*/](/*arg block*/) /*opt mutable, except*/ -> /*return type*/
    { /*body*/ }
    //Example:
    auto square = [](double x) -> double { return x*x; };
```
* By default `operator()` of lambda expressions is `const`.
* To disable implicit `const`, use keyword `mutable`
* Capture List:
    * `[=]` Capture all by value
    * `[&]` Capture all by reference
    * `[=, &var]` Capture all by value, except `var`
    * `[this]` Capture all members.
    * `[=, &var]` Capture all by value, except `var`
* Within a lambda, private members will be accessible if accessible in the calling method.

