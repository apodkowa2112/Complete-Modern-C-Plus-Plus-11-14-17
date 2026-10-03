# OOP Inheritance & Composition
## Composition
* Object within other object
* "has-a" relation
## Inheritance:
* inherits features of another class.
* Represent "is-a" relationship.
* `class Dog : public Animal`
* Specific overloads prioritized over inherited overloads
* `()`
## Access Modifiers:
* `private`: Inaccessible
* `public`: Accessible
* `protected`: accessible only to child.
* `class Child : public Base`: Base public and protected members accessible to Child, private inaccessible. Good default.
* `class Child : protected Base`: Same as public above, but `Base::public`->`Child::protected`
### Object Construction
* Constructors execute from base-->child
* Destructors execute from child-->base

## Banking Application
* Manage accounts
* Customers can perform common operations
* Banks can perform administrative tasks
* Accounts specialized as checking and savings.

Savings account spec:
* Interest rates
* GetInterestRate()
* AccumulateInterest();

## Inheriting Constructors
If you:
* Have no new members in the child class
* Want to use all the base class constructors
Then use `using Base::Base` will inherit the constructor behavior.

## virtual Keyword
* `virtual` deprioritizes base class implementation of a method in favor of a child class when the function signature is of the base class.
    * Example: `int Base::foo() virtual;` means prefer `Child::foo();`
* virtual is a polymorphic concept.
* Derived overloads are called polymorphic functions.
* Specific call may be resolved at compile time or runtime.
* Polymorphic functions implemented by pointer/reference.
* Array of virtual function pointers called a virtual table:
```cpp
// In child class
&Account::GetInterestRate(); // declared virtual in Account
```
* Base class should always have a virtual destructor, so that child destructors are always invoked under typecasts to Base.
* To prevent derivations of a class, use the `final` keyword in declaration: `class Zip final {/*...*/}`
* The `override` keyword can be used in a Child function member to check if the Base class has an identical function signature.
* For a non-final class, you can prevent a particular method from being overidden by specifying `overide final`.
## typeid
* `#include <typeinfo>`
* Use case, have pointer to Base class, want conditional logic to specific object.
```cpp
#include <iostream>
#include <typeinfo>

class Base { 
    virtual int foo() { return 0; }; // virtual required: Base needs a vtable for typeid to figure out the derived class.
} ;
class Child : public Base {};

int main () {
    using namespace std;
    Child c;
    Base* b = &c;

    cout << "c:\t"  << typeid( c).name() << endl; // i.e. Child
    cout << "b:\t"  << typeid( b).name() << endl; // i.e. Base *
    cout << "*b:\t" << typeid(*b).name() << endl; // i.e. Child
}
```
## dynamic_cast
* `dynamic_cast` performs a cast from Base* ==> Derived* if possible.
* if not possible, it will return a `nullptr`
* for references, if not possible, it will throw an `bad_cast` exception.
* generally prefer `typeid` instead of `dynamic_cast`, but better to avoid both if possible.
## Abstract class
* If you want to force child classes to implement `foo()` make `Base::foo()` a pure virtual function:
```cpp
class Base {
    virtual void foo() = 0;
};
```
* Must be overridden by derived classes.

## Diamond Inheritance
```
  +------>ChldA----+
  |                |
  |                v
Parent          GrndChld
  |                ^
  |                |
  +------>ChldB----+
```
* `GrndChld` inherits two copies of `Parent` in its vtable.
* If you try to use a Parent method under this situation, you will get a compiler error.
