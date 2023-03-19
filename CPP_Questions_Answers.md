# What is dynamic binding

- In C++, dynamic binding, also known as runtime polymorphism or late binding, is a feature that allows a program to determine which function to call at runtime based on the type of the object being used. It allows a derived class to override a method of its base class so that the method called depends on the type of the object at runtime, rather than at compile time.
- Dynamic binding is achieved through the use of virtual functions. A virtual function is a member function of a base class that can be overridden by a derived class. When a virtual function is called using a pointer or reference to an object of a derived class, the function that is executed is determined at runtime based on the actual type of the object.
- Dynamic binding is useful in situations where you want to provide a common interface for a set of related classes, but allow each class to implement the interface in its own way. This allows you to write code that works with objects of any of the related classes, without having to know the exact type of the object at compile time.

# What is function overload resolution

- Function overload resolution is a process in C++ where the compiler determines which function to call when there are multiple functions with the same name but different parameters. This process is also known as function overloading.

- When a function is called in C++, the compiler looks for a function with the same name and the correct number and types of parameters. If there is only one such function, that function is called. However, if there are multiple functions with the same name, the compiler needs to determine which one to call based on the arguments passed to the function.

The process of function overload resolution involves several steps:

1. The compiler creates a set of candidate functions that have the same name as the function being called.

2. The compiler eliminates any functions that are not viable based on the number or types of arguments being passed.

3. The compiler ranks the remaining functions in the set based on a set of rules defined by the language standard. These rules include considerations such as the exact match of arguments, conversion of arguments, default arguments, and the use of template arguments.

4. If there is a clear best match, that function is called. If there are multiple functions that are equally good matches, the compiler generates an error.

- Function overload resolution allows programmers to define multiple functions with the same name, making their code more readable and intuitive. It is an important feature of C++, as it allows for more flexibility and expressive power when designing software.

# What is user defined conversion

- User-defined conversions in C++ refer to the process of defining a conversion function within a class to enable the object of that class to be converted to another type. This process is also known as type conversion or type casting.

- In C++, you can define a user-defined conversion function using the syntax:

```CPP
operator target_type() const;
```
> where target_type is the type you want to convert your class to. This function can be defined as a member function of the class or a non-member function that takes an object of the class as its argument.

- For example, consider the following class:

```CPP
class MyInt {
public:
    int value;
    MyInt(int v) : value(v) {}
};
```
- To enable objects of this class to be converted to integers, we can define a user-defined conversion function like this:

```CPP
class MyInt {
public:
    int value;
    MyInt(int v) : value(v) {}
    operator int() const { return value; }
};

```
- This allows us to use objects of the MyInt class as if they were integers, such as:

```CPP
MyInt x(42);
int y = x;

```
> In this example, the user-defined conversion function operator int() const is called to convert the object x of the MyInt class to an integer y.

- User-defined conversions can be powerful tools in C++, but they should be used with caution as they can sometimes lead to unexpected results and make code harder to read and maintain. It is generally recommended to use them sparingly and only when they make the code more readable and understandable.







