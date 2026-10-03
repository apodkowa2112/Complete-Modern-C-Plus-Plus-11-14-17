# enums
* enums can implicitly convert to an integer, but not the other way around.
* Traditional enums have global scope. Cannot redefine `foo::RED` and `bar::RED`.
* enum class scopes them to a namespace to prevent collision. They also cannot be implicitly converted to their underlying type.

# strings
Potential pitfalls with C-strings:
* Need to know the lengths
* Need to remember to null termination
* Need to remember when to call delete/free and which one.
Can be necessary for C-library compatibility.

## std::string
Useful methods:
* `erase()`
* `clear()`
* `length()`
* `find()`
* `c_str()`
```cpp
    int pos = str.find("World", 0);
    if (pos != std::string::npos) std::cout << "Found string" << std::endl;
```

## stringstreams

```cpp
#include <sstream>

int main() {
    std::stringstream ss; // I/O
    std::istringstream is; // I only
    std::ostringstream os; // O only

    ss << "foo" << "bar" <<  2000;
    std::string s = ss.str();

    std::string data = "2 3 5";
    ss.str(data);
    int a;
    while (ss >> a) std::cout << a << std::endl;
}
```

## User-defined Literals
* Hard-coded variables
* examples:
    * 14u,
    * 621l
    * 9.2f
    * L"wide string"
* Can define a "unit" suffix in code: `98.6_F`
* `<return type> operator "" _<literal>(<args>)`
* valid `<args>`:
    * integer -> unsigned long long
    * floating point -> long double
    * charactor -> char, wchar_t, char16_t, char32_t
    * string -> const char*
* Literals need to have an underscore. Without underscore is reserved for STL.

## constexpr
* compile time evaluated expression.
* only accepts literal types: void, POD types, references, arrays...
* can only accept a return statement in (C++11). C++14 has relaxed rules, including multiple conditionals, but they are complex.
* constexpr variables are a subset of const variables that can only be initialized at compile time.

## std::initializer_list
Uniform initialization: `int x{42};`
* `#include <initializer_list>`
* `std::initializer_list<int> data = {1, 2, 3};`
* Implicitly constructed with braced list.

```cpp
class Bag {
public:
    Bag(std::initializer_list<int> values ) {
        for (auto it = values.begin(); it != values.end(); ++it) {
            Add(*it);
        }
    }
    void Add(int value);
    int operator[](int index);
    int size();
}
```

## union
Representing all members in the same memory to save space.
Disadvantages:
* Type ambiguity
* non-default destructors deletes the default constructor
* cannot assign objects of user-defined types directly to a union member.
* user-defined types are not destroyed implicitly
* Can't have a base class.
* Cannot be derived from.
Size will be the maximum of all the members.
placement new operator needs to be used to initialize union variables manually:
```cpp
union UDT {
    A a;
    B b;
    UDT() {}
    ~UDT() {}
}

int main() {
    UDT u;
    new(&udt.a) A{};
}
```

