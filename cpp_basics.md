1. In c++, if we do not write our own, the compiler will automaticly create a default constructor, copy constructor and an assignment operator for every class
2. When a copy constructor wil be called?
   - when an object of a class is return by value
   - when an object of a class is passed by value as argument
   - when an object is constructed based on another object of the same class
   - when compiler generate a temporary object
3. We must use initializer list in a constructor when
   - For initialization of non-static const data members
   - For initialization of reference members
   - For initialization of member objects which do not have default constructor
   - For initialization of base class members
   - When constructor’s parameter name is same as data member
4. Why copy constructor argument should be const in C++?
   - One reason for passing const reference is, we should use const in C++ wherever possible so that objects are not accidentally modified
5. Implicit return type of a class constructor is the class type itself
6. 
