# Operator Overloading

* operators can be implemented as methods or as global functions.
* methods have the benefit of private member/method access for performance optimizations
* global functions have the benefit of not needing to modify the class internals, which would be needed when interacting with a closed source API

Example syntaxes:
Method:
```cpp
class foo{
public:
    foo operator+(objB); // foo sum = objA + objB;
}
```
Global:
```cpp
foo operator+(foo objA, foo objB);
```
## Method overloads:
Syntax: 
```cpp
    retType operator<opType>(argType arg); // retType ret = opType(obj, arg);
```
The object does not need to be included in the argument list, unlike global functions.
Examples:
```cpp
class foo {
public:
    foo & operator++(); // preincrement
    foo operator+(objB); // foo sum = objA + objB;
}
```
Postincrement uses the convention of adding a dummy `int` argument:
```cpp
class foo {
public:
    foo& operator++(int); // postincrement, int argument is dummy and not called
}
```
The postincrement operator typically returns a reference to a temporary variable, which is cleaned up when the expression terminates. Postincrement was necessary for abstraction drop-in compatibility with existing C idioms for integers and pointers (i.e. `*dst++ = *src++`, `arr[i++] = j`, etc).

## Global Members
When operators work within public access limitations, the specification is straightforward.
When operators need private member access, they must be declared as friend functions within the class declaration:
```cpp
public:
    friend foo operator+(foo objA, foo objB);
}
```
This means that only the header file needs modifications, and compiled translation units can be stay unmodified.
Generally these should be used as a method of last resort.
Similarly classes may be made friends as well (i.e. a `Printer` class).

## Smart Pointers
Motivating example:
```cpp
void CreateInteger() {
    Integer *p = new Integer;
    cout << p << endl; 
    // No delete, so destructor never called.
}
```
Idiom: RAII
```cpp
class IntPtr {
    Integer *m_p;
public:
    IntPtr(Integer *p) : m_p(p) {}
    ~IntPtr() { delete m_p; }
    Integer *operator->() { return m_p; } 
    Integer *operator*()  { return *m_p; } 
}
```

STL smart pointer library: `memory`
`unique_ptr` has move semantics, but not copy semantics.
`shared_ptr` implements reference counting to trigger the destructor.

## Rules
* associativity precedence and nArgs do not change
* Operators (except new & delete) are non-static
* Only predefined operators allowed.
* Global overload must be used if the first operator is primitive (i.e. int)

## Type Conversions
* `static_cast` prevents invalid casts
* `reinterpret_cast` allows invalid casts but preserves qualifiers (i.e. `const`)
* `explicit` prevents a parameterized constructor to be called during an assignment operation without an explict type cast.
* Type conversion operator syntax: `operator type ()`, i.e. `operator int()` Note that there is no return type.
* `explict` can disable implicit casting for Type conversion operators as well.

## Initialization vs Assignment:
* Initialization: `Integer a {5};`
* Assignment: `Integer a = 5;`
* Assignment has additional constructor and destructor overhead resulting from the implicit type conversion. 
