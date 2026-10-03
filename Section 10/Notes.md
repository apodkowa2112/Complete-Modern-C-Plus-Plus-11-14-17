# Exception handling.

* Unlike C-style errors, exceptions cannot be ignored.
* Require immediate handling to prevent a crash
* std::exception contains a `what()` method that returns the error message string.
* `try {} catch (std::exception &ex){}`
* Special std::exceptions:
    * `runtime_error`: rather generic.
    * `out_of_range`: for exceeding array bounds
    * `bad_alloc`: for memory errors, if `new` fails, `vector` fails, etc.
* Can use `catch (...)` to handle custom exceptions.
    * Not very useful.
    * Should be last catch block if used at all.
## Stack Unwinding
* Destructors for local objects will be destroyed when exceptions are called.
* For pointers, `delete` calls may be skipped, leading to memory leaks.
* Smart pointers will get their destructors called, so should be used.
## Constructors and Destructors
* If an exception is thrown in a constructor, the destructor will not be called.
* If an exception is thrown in a destructor, the program will crash unless handled appropriately.

## noexcept
* Needed in declaration and definition.
* exception from noexcept function terminates the program
* Undefined behavior: stack may not be unwound when an exception in noexcept function occurs.
* functions calling other functions should not be noexcept due to lack of control.
```cpp
int Sum(int x, int y) noexcept(/*true*/) {return x+y;}
```
* `noexcept (false)` explicitly tells the compiler that exceptions are possible.
* `noexcept(foo())` tells the compiler to check if exceptions are possible in `foo()`
* All destructors are implicitly marked `noexcept`.
* move constructors should have `noexcept(true)`
