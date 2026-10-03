# Refactoring Raw pointers to unique_ptr
These are equivalent:
```cpp
foo* p;                 p = new foo{value};
std::unique_ptr<foo> p; p.reset( new foo{value} );
```

```cpp
void bar( foo* p );
foo* p;                 bar(p);
std::unique_ptr<foo> p; bar(p.get());
```
Cannot pass `unique_ptr` by value unless you `std::move` it.

`shared_ptr::use_count()` can be used to print the reference count.

## weak_ptr

`weak_ptr` knows the reference count of a `shared_ptr` and doesn't increment it when initialized.
`weak_ptr::expired()` tells you if the `shared_ptr` has been destroyed.
`weak_ptr::lock()` will give you a `shared_ptr` handle, which will increment the reference count.

```cpp
class Employee;
class Project{
public:
    std::shared_ptr<Employee> m_emp;
}
class Employee {
public:
    std::shared_ptr<Project> m_prj;
}

int main() {
    str::shared_ptr<Employee> emp{new Employee};
    str::shared_ptr<Project> prj{new Project};
    
    emp->m_prj = prj;
    prj->m_emp = emp;
    // Memory leak! Resources never destroyed because reference counts never go to 0.
}
```
Solution: Use `std::weak_ptr` for the members.

## Deleter
Legacy code and C-code use malloc/free for allocation.
By default, smart pointers use `new/delete`, which is not compatible with `malloc/free`
Supports
Can also use to fopen/fclose a file handle.
```cpp
  auto file = std::unique_ptr<FILE, int(*)(FILE*)>(
      fopen("test.txt", "w"), fclose);
```

## Dynamic arrays
```cpp
    std::unique_ptr<int> p{new int[]{1,2,3,4,5}}; 
    // deleter calls delete int, not delete int[5] possible undefined behavior
    // smart pointers don't support p[0] syntax.
```
Fix:
```cpp
    std::unique_ptr<int[]> p{new int[]{1,2,3,4,5}}; // C++17 only.
    // better idea: just use std::vector
```

## Make functions
```cpp
    std::unique_ptr<int> p{new int{5}};
    auto p = std::make_unique<int>(5); // better
```
