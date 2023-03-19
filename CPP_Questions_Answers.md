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

# What is inline expension

- Inline expansion in C++ is a feature that allows the compiler to replace a function call with the actual code of the function at the point where the function is called. This is done by using the inline keyword to suggest to the compiler that the function should be expanded inline.
- When a function is called normally in C++, the program must save the current execution context and jump to the code of the function. After the function completes, the program must restore the execution context and continue executing from where it left off. This process incurs some overhead, particularly for small, frequently called functions.
- By using the inline keyword, the compiler is instructed to replace the function call with the actual code of the function at the point where the function is called. This can reduce the overhead of the function call and improve performance, particularly for small, frequently called functions.

**For example, consider the following code:**
```CPP
inline int square(int x) {
    return x * x;
}

int main() {
    int result = square(5);
    return 0;
}
```
- In this example, the square() function is marked as inline using the inline keyword. When the function is called in the main() function, the compiler will replace the function call with the actual code of the function, resulting in code that is equivalent to:

```CPP
int main() {
    int result = 5 * 5;
    return 0;
}

```
> This can result in faster and more efficient code, particularly for small, frequently called functions.

- It's worth noting that the use of inline is a suggestion to the compiler, and the compiler may choose to ignore the suggestion if it determines that inlining the function would not be beneficial. Additionally, inlining can result in larger executable size, so it should be used judiciously, particularly for larger functions.

# What is loop unrolling

- Loop unrolling in C++ is an optimization technique where the compiler replaces a loop with a sequence of instructions that perform the same operation multiple times. This reduces the overhead of loop control, such as loop counter updates and conditional branches, and can result in faster and more efficient code.

- In loop unrolling, the compiler takes a loop that looks like this:

```CPP
for (int i = 0; i < n; i++) {
    // loop body
}

```
- And transforms it into a sequence of instructions that look like this:

```CPP
for (int i = 0; i < n; i += 4) {
    // loop body for i
    // loop body for i + 1
    // loop body for i + 2
    // loop body for i + 3
}

```
- In this example, the loop has been unrolled by a factor of 4, meaning that the loop body is executed 4 times for each iteration of the loop counter. This can improve performance by reducing the overhead of the loop control instructions.

- Loop unrolling is particularly effective for loops with a small number of iterations, as the overhead of loop control can dominate the actual work performed by the loop. However, unrolling a loop can also increase the size of the code, so it should be used judiciously and only when it is likely to provide a performance benefit.

- In C++, loop unrolling can be performed automatically by the compiler using various optimization flags or manually by the programmer using techniques such as template metaprogramming or recursion.

# is "loop unrolling" an inline expension?

- Loop unrolling is not the same as inline expansion, although they are related optimization techniques that can improve the performance of C++ code.
- Inline expansion involves replacing a function call with the actual code of the function at the point where the function is called, which can reduce the overhead of the function call and improve performance. On the other hand, loop unrolling involves replacing a loop with a sequence of instructions that perform the same operation multiple times, which can reduce the overhead of loop control and improve performance.
- While both techniques can result in faster and more efficient code, they are applied at different levels of the code. Inline expansion is applied to functions, while loop unrolling is applied to loops. Additionally, inline expansion is performed automatically by the compiler when the function is marked as inline, while loop unrolling can be performed automatically or manually by the compiler or the programmer.
- In summary, loop unrolling and inline expansion are distinct optimization techniques that can be used together or separately to improve the performance of C++ code.

# what is generic programming paradigm

- Generic programming is a programming paradigm in C++ that emphasizes the creation of reusable code that can work with multiple data types and data structures. In this paradigm, algorithms and data structures are designed in a way that is independent of the specific types of data they will be used with, allowing them to be reused with different types of data.

- The key features of generic programming in C++ include templates, function objects, and generic algorithms.

- **Templates:** Templates are a powerful feature in C++ that allow you to define functions and classes that work with multiple data types. A template is a blueprint for creating a function or class, with placeholders for the actual data types to be used. When the template is instantiated with specific data types, the compiler generates the appropriate code.

- **Function Objects:** Function objects, also known as functors, are objects that behave like functions. They can be defined with templates and can work with multiple data types. Function objects are often used with generic algorithms to provide customized behavior.
- **Generic Algorithms:** Generic algorithms are algorithms that can work with different data types and data structures. Examples include sorting, searching, and copying algorithms. Generic algorithms are designed to work with any data type that meets certain requirements, such as being iterable.

- By using templates, function objects, and generic algorithms, C++ allows you to write reusable code that can work with a wide range of data types and data structures. This can result in more efficient and flexible code, as well as reducing the amount of code duplication.

# so what is "paradigm" exactly

- In computer programming, a paradigm is a fundamental style or approach to designing and coding software systems. It is a set of principles and practices that guide the programmer in solving problems and creating software solutions.

- Different paradigms have different approaches to organizing code, structuring data, and defining relationships between program components. Some common paradigms in programming include:

- **Procedural programming:** A paradigm in which programs are composed of procedures or functions that perform specific tasks.

- **Object-oriented programming:** A paradigm in which programs are composed of objects that have data and behavior, and can interact with each other through messages or methods.

- **Functional programming:** A paradigm in which programs are composed of functions that are treated as first-class objects, and can be used to compose other functions.

- **Event-driven programming:** A paradigm in which programs are driven by events, such as user input or system notifications, that trigger specific actions or functions.

- Each paradigm has its own strengths and weaknesses, and is best suited for different types of problems and software systems. Programmers may choose to use one or more paradigms in a given project, depending on the requirements and constraints of the project.

# so when i declare a function with "inline", then  i say "compiler, just use the declaration of this function here"

- Yes, when you declare a function with the inline keyword in C++, you are essentially telling the compiler to substitute the function call with the actual body of the function at the call site (where the function is called), instead of generating a separate function call instruction.

- This can result in faster code execution because the overhead of calling a function (such as pushing and popping values on the stack) is eliminated, and the compiler can perform additional optimizations on the inlined code.

- However, it's important to note that the inline keyword is just a hint to the compiler, and it's up to the compiler to decide whether to actually inline the function or not. Additionally, inlining a function can lead to larger executable size and longer compilation times, so it's typically best to use inline judiciously and only for small, frequently-used functions.


# why the functions which is declared in classes are implicitly inline?

- In C++, member functions declared inside a class definition are treated as inline functions by default. This is because member functions defined inside a class are usually small and frequently used, and the overhead of a function call can be significant for performance-critical code. By defaulting to inline, the compiler can optimize the code by eliminating the overhead of a function call and potentially generating more efficient code.

- Note that this behavior only applies to member functions that are defined inside the class definition, not to functions that are merely declared inside the class definition and later defined outside the class definition. If you define a member function outside the class definition, you can still mark it as inline explicitly using the inline keyword, or the compiler may choose to inline it anyway based on its own optimization decisions.

# Why do i have to say to compiler something like that with inline keyword? Compiler thinks more efficient than human brain

- While it's true that modern compilers are very sophisticated and can perform many optimizations automatically, there are still cases where providing hints to the compiler can improve the efficiency of the resulting code. Inlining is one such case.

- Even though a compiler may be able to determine on its own that a function should be inlined, providing the inline keyword explicitly can serve as a stronger hint to the compiler that inlining is desirable. This can be especially useful in cases where the function is larger or more complex than the compiler's threshold for automatic inlining, or in cases where you want to ensure that a particular function is inlined even if the compiler might not have chosen to inline it automatically.

- In addition to providing hints to the compiler, the inline keyword also serves as a signal to other programmers who read the code that the function is designed to be inlined and that it may be called frequently. This can help improve the readability and maintainability of the codebase.

# Even though "not inlining"more efficient, when i declare it an inline function, what compilers do in thsat situation?

- When you declare a function as inline in C++, it is essentially a request to the compiler to consider inlining the function. However, the compiler may choose to ignore the request and generate a non-inlined function for various reasons.

- For example, if the function is too large or complex to be inlined efficiently, the compiler may decide not to inline it. Additionally, if the function is not frequently called, or if it is used in a context where inlining would not improve performance, the compiler may choose not to inline it.

- In cases where the compiler does not inline a function that has been declared as inline, the function will be treated as a regular non-inline function, and a separate function call instruction will be generated whenever the function is called. In other words, declaring a function as inline does not guarantee that it will be inlined, but it does give the compiler the option to inline it if it deems it appropriate.

# If there is a function declared in class with a huge code, will compiler still use it like an inline function?

- The inline keyword in C++ is just a hint to the compiler to consider inlining the function, but it does not guarantee that the function will be inlined. The decision to inline a function or not is ultimately up to the compiler, and is based on a variety of factors, including the size and complexity of the function, the number of times it is called, and the optimization settings of the compiler.

- If a member function of a class has a large and complex code, it is possible that the compiler may decide not to inline it, even if it is declared with the inline keyword. In such cases, the function will be treated as a regular non-inline function, and a separate function call instruction will be generated whenever the function is called.

- It's worth noting that even if the compiler decides not to inline a function that is declared as inline, the function can still be optimized in other ways, such as through function-level optimization or link-time optimization. Additionally, modern compilers are able to make increasingly sophisticated decisions about inlining, and may choose to inline even large or complex functions in certain circumstances.

# what is one definition rule (ODR)

- The One Definition Rule (ODR) is a fundamental rule in C++ that specifies that every entity (such as a variable, function, or class) in a C++ program must have exactly one definition across all translation units in which it is used. In other words, if a particular entity is defined in more than one translation unit, the program has undefined behavior.

- The ODR is enforced by the linker, which is responsible for resolving symbols (such as function or variable names) across multiple object files and libraries to create a final executable. If the linker encounters multiple definitions of the same entity, it will produce an error and fail to create the executable.

- To adhere to the ODR, it is common practice to declare entities in header files and define them in source files, to ensure that they are only defined once across all translation units that use them. Additionally, C++ provides several mechanisms for controlling the visibility of entities across translation units, such as the static keyword for variables and functions, and the inline keyword for functions.

# so what will happen when i use inline keyword? Does it adhere to the ADR?

- When you use the inline keyword on a function in C++, it does not affect the One Definition Rule (ODR). The ODR still applies, and every entity (including functions) must have exactly one definition across all translation units in which it is used.

- However, the inline keyword does provide a way to define a function in a header file, which can be included in multiple translation units without violating the ODR. This is because the inline keyword tells the compiler that the function definition may be replicated in multiple translation units, and that it should be treated as a candidate for inlining instead of generating a separate function for each translation unit.

- If a function is declared as inline and defined in a header file that is included in multiple translation units, the compiler will typically generate identical copies of the function code in each translation unit, but the linker will treat them as a single function definition. This is because the inline keyword effectively allows the function to be defined multiple times, as long as each definition is identical, and as long as the function is not odr-used (that is, its address is not taken).

- Therefore, using the inline keyword can help to avoid linker errors when defining functions in header files, but it does not exempt them from the ODR.

# what does mean constexpr keyword 

- The constexpr keyword in C++ is used to indicate that a variable or function can be evaluated at compile-time, and its value will be a constant expression. This means that the value of a constexpr variable or function is known at compile-time, and it can be used in contexts where a constant expression is required, such as array sizes, template arguments, and switch statements.

- Variables declared as constexpr must be initialized with a constant expression, and the value of the expression must be computable at compile-time. Functions declared as constexpr must have a single return statement, and their parameters and return types must also be able to be evaluated at compile-time.

**Here is an example of using constexpr:**

```CPP
constexpr int factorial(int n) {
    return (n <= 1) ? 1 : (n * factorial(n-1));
}

int main() {
    constexpr int n = 5;
    int arr[factorial(n)]; // array size is computed at compile-time
    return 0;
}

```
> In this example, the factorial function is declared as constexpr, which means it can be used in a context where a constant expression is required. In main, the n variable is declared as constexpr, and the array size is computed using the factorial function at compile-time.

- Using constexpr can help improve performance and reduce memory usage, as the values of constants are known at compile-time, and do not need to be computed at run-time.

# what is happening if i use constexpr in function definition

- If you use the constexpr keyword in a function definition in C++, it means that the function is a candidate for evaluation at compile-time. This means that the function may be used to compute a constant expression, and its result will be a compile-time constant.

- If a function is declared as constexpr and its arguments are also constant expressions, then the function may be evaluated at compile-time. In this case, the function is evaluated by the compiler during the compilation process, and the result is substituted directly into the code that uses the function.

**Here is an example of using constexpr in a function definition:**

```CPP
constexpr int add(int x, int y) {
    return x + y;
}

int main() {
    constexpr int a = 5;
    constexpr int b = 7;
    constexpr int c = add(a, b); // evaluated at compile-time
    return 0;
}

```

- In this example, the add function is declared as constexpr, and it takes two integer arguments. In main, the a and b variables are declared as constexpr, and the add function is called with a and b as arguments to compute c. Since a and b are constant expressions, the add function is evaluated at compile-time, and its result is substituted directly into the code.

- Using constexpr in function definitions can help to improve performance and reduce memory usage, as constant expressions are known at compile-time and do not need to be computed at run-time. However, it is important to note that not all functions can be declared as constexpr. Functions that perform I/O, use dynamic memory allocation, or have side effects cannot be evaluated at compile-time and cannot be declared as constexpr.

# compiler know how to improve performance better than me. So why do we using constexpr

- You are correct that the compiler knows how to optimize code better than most programmers. However, there are situations where the use of constexpr can provide benefits beyond what the compiler can do on its own.

- One major advantage of constexpr is that it allows certain computations to be performed at compile-time instead of run-time. This can lead to faster execution times and reduced memory usage. For example, imagine that you have a function that computes a hash value at run-time, which is called frequently throughout your program. By making the function constexpr, the hash computation can be done once at compile-time, and the result can be substituted into the program code, rather than re-computing the hash each time the function is called.

- Another advantage of constexpr is that it provides compile-time error checking for certain types of computations. For example, if you have a function that computes the size of an array based on its contents, you can make the function constexpr to ensure that the computation is performed at compile-time, and that any errors in the computation will be caught by the compiler before the program is even run.

- Finally, the use of constexpr can make code easier to understand and maintain, especially in cases where a constant value is used in multiple places throughout the program. By making the value constexpr, you can ensure that it is only computed once, and that all uses of the value are consistent with each other.

- Overall, while the compiler is certainly capable of optimizing code on its own, the use of constexpr can provide additional benefits in terms of performance, error checking, and code maintainability.

# so once i use constexpr in function definition, i made it to be calculated in compile time right

- Yes, that's correct. When you use the constexpr keyword in a function definition, you are telling the compiler that the function can be evaluated at compile-time for constant expressions, which means that the result of the function can be computed by the compiler before the program is even run.

- This can be useful for performance optimization, as it avoids the overhead of runtime function calls, and can also help catch errors at compile-time rather than runtime. Additionally, constexpr functions can be used in other contexts where constant expressions are required, such as array sizes or template arguments.

# what are differences between class and structs

- In C++, class and struct are both used to define custom data types, but they have some differences in terms of their default access control and inheritance.

- The primary difference between class and struct is in their default access control. In a class, the default access level is private, meaning that all members declared within the class are by default private, unless otherwise specified. In contrast, in a struct, the default access level is public, meaning that all members declared within the struct are by default public, unless otherwise specified.

- Another difference is in their use for inheritance. When using class, the base class inheritance is by default private, while when using struct, it's public. You can use the public, private and protected access modifiers to specify the level of access for members and inheritance in both class and struct.

- In terms of their capabilities, class and struct are almost identical. Both can contain member functions, constructors, destructors, and data members. They can both be used to define objects, and can be used interchangeably in most cases.

- In practice, the choice between class and struct is largely a matter of style and convention. In some coding communities, it's common to use struct for simple data structures that don't have much behavior, and class for more complex objects with behavior and encapsulation. However, this is just a convention and you can use either class or struct depending on your coding style and preference.

# In game developments, which one i should use?

- In game development, there is no clear preference for using either class or struct. Both can be used effectively depending on the situation.

- In general, class tends to be used for more complex objects with behavior, encapsulation, and inheritance, such as player characters, enemies, or game items. struct tends to be used for simple data structures that don't have much behavior or encapsulation, such as vectors, points, or colors.

- However, these are just conventions and there is no hard and fast rule. Ultimately, the choice between class and struct should be based on what best fits the needs of your specific game development project, and what coding style you are most comfortable with.

# which situations are suitable for class and for structs?

- In general, class and struct can be used interchangeably in most cases in C++. However, there are some general guidelines on when to use each:

**Use class when:**

1. You need to define an object with complex behavior, encapsulation, and inheritance.
2. You need to use access modifiers to protect the data members and member functions of the class.
3. You want to define constructors, destructors, and overloaded operators.

**Use struct when:**

1. You need to define a simple data structure that groups together related variables.
2. You don't need encapsulation, and the data members can be public.
3. You don't need constructors, destructors, or overloaded operators.

**Here are some examples to illustrate these guidelines:**

**Use class:**

```CPP
class Player {
private:
    std::string name;
    int health;
public:
    Player(std::string name, int health);
    void attack(Player& other);
    void takeDamage(int damage);
};

class Enemy : public Player {
public:
    Enemy(std::string name, int health, int attackPower);
    void attack(Player& other);
private:
    int attackPower;
};

```

**Use struct:**
```CPP
struct Vector3 {
    float x, y, z;
};

struct Color {
    unsigned char r, g, b, a;
};

struct Point {
    int x, y;
};

```
- Of course, these are just guidelines and there can be exceptions. The choice between class and struct should ultimately depend on the specific needs and requirements of your program.

# Why they declare function in class and define it out of the class?

- In C++, it is common to declare a function inside a class using a function prototype, and then define the function outside the class. This is known as "separate compilation" or "separate linkage" and is often done for code organization and maintainability purposes.

**Here are some reasons why you might want to declare a function in a class and define it outside of the class:**

1. Code organization: By grouping related functions together in a class, it can be easier to read and understand the code. Declaring the function inside the class provides a clear indication that the function is related to the class, while defining it outside the class provides a separation of concerns.

2. Encapsulation: By declaring functions as public, protected, or private inside a class, you can control the access to the functions and data members. This helps to enforce encapsulation and maintain the integrity of the class.

3. Modularity: By defining functions outside of the class, you can use them in other classes or functions, promoting code reuse and modularity.

4. Compilation time: By separating the declaration and definition of functions, the compiler can process each separately, reducing compile time and making the code easier to maintain.

**Here is an example of declaring a function in a class and defining it outside of the class:**

```CPP
class MyClass {
public:
    void myFunction(); // function prototype
};

void MyClass::myFunction() { // function definition outside of class
    // function body
}

```
- By declaring the myFunction() inside the MyClass, you can use it as a member function of MyClass. By defining it outside the class, you can separate the implementation of the function from the declaration, making it easier to maintain and reuse.

# what is "this" keyword

- In C++, the this keyword is a pointer that refers to the current instance of a class. It is used inside a member function of a class to refer to the object on which the member function is being called.

- When a member function is called on an object, the object's address is automatically passed to the this pointer. The this pointer can be used to access the object's data members and member functions.

- Here is an example of using the this pointer inside a member function:

```CPP
class MyClass {
public:
    void setX(int x) {
        this->x = x; // using this pointer to access object's data member
    }
private:
    int x;
};

int main() {
    MyClass obj;
    obj.setX(5); // calling setX function on obj
    return 0;
}

```

> In this example, the setX() member function is called on an object obj. Inside the setX() function, the this pointer is used to refer to the obj object and access its x data member.

- When a member function is called on an object, the this pointer points to the memory location of that object. Within the member function, the this pointer can be used to access the object's data members and other member functions.

# what is const correctness

- Const correctness in C++ refers to the practice of using const to enforce read-only access to data, and to ensure that member functions do not modify the object's state if they are not intended to do so.

- The const keyword is used to declare that a variable or member function does not modify the object's state. When applied to a variable or parameter, const indicates that the value of the variable cannot be modified after it is initialized. When applied to a member function, const indicates that the function does not modify the object's state.

**Here is an example that demonstrates const correctness:**

```CPP
class MyClass {
public:
    int getValue() const {
        return value;
    }
    void setValue(int value) {
        this->value = value;
    }
private:
    int value;
};

int main() {
    const MyClass obj; // obj is a const object of MyClass
    int value = obj.getValue(); // read-only access is allowed
    obj.setValue(10); // compilation error: setValue() is not a const function
    return 0;
}

```

> In the above example, getValue() is declared as a const member function, which means it cannot modify the object's state. Therefore, it can be called on a const object like obj. On the other hand, setValue() is not declared as const, which means it can modify the object's state. Therefore, it cannot be called on a const object.

# what is mutable keyword

- In C++, the mutable keyword is used to specify that a member variable of a class can be modified even if the object is const. This allows a const object to modify its state in a controlled manner.

**Here is an example to demonstrate the use of mutable:**

```CPP
class MyClass {
public:
    int getValue() const {
        counter++; // modify mutable member
        return value;
    }
private:
    int value;
    mutable int counter = 0; // mutable member
};

int main() {
    const MyClass obj; // obj is a const object of MyClass
    int value = obj.getValue(); // counter is incremented, but obj is still const
    return 0;
}

```
> In the above example, counter is declared as mutable, which means it can be modified even if the object is const. The getValue() function increments the counter member, but because it is marked as mutable, this modification is allowed even if the object is const. Note that modifying a non-mutable member of a const object is not allowed and will result in a compilation error.

# what is static initialization fiasco

- The "static initialization fiasco" is a term used to describe a class of bugs that can occur in C++ programs when the order of initialization of global variables is not well-defined or not understood.

- In C++, global variables that are defined in a single translation unit are initialized in a well-defined order. However, when global variables are defined in multiple translation units, the order of initialization is not well-defined, and may depend on factors such as the order of linking of the translation units.

- When the initialization of one global variable depends on the value of another global variable that has not yet been initialized, this can result in undefined behavior. For example, consider the following code:

```CPP
// file1.cpp
#include <iostream>
extern int x;
int y = x + 1;

// file2.cpp
#include <iostream>
int x = 42;

// main.cpp
#include <iostream>
extern int y;
int main() {
    std::cout << y << std::endl;
}

```
> In this example, the y variable in file1.cpp depends on the value of the x variable defined in file2.cpp. However, the order of initialization of global variables is not well-defined, so it is possible for y to be initialized before x, resulting in undefined behavior. In the example code I provided, it is an undefined behavior.

> The reason is that the order of static initialization of non-local static objects defined in different translation units is unspecified. It means that it is not guaranteed that the variable x defined in a.cpp will be initialized before the variable y defined in b.cpp when the program starts. Therefore, if the initialization of y depends on the value of x, the behavior of the program is undefined.

- To avoid the static initialization fiasco, it is recommended to avoid global variables as much as possible, and to use local static variables or singleton patterns instead, as these provide more control over the order of initialization.

- To avoid the static initialization fiasco, we can use techniques such as lazy initialization or initialization-once to ensure that the variables are initialized in a well-defined order.

# What are new and delete operators

- new and delete are the dynamic memory management operators in C++. They are used to allocate and deallocate memory on the heap.

- new operator is used to allocate memory dynamically for objects at runtime. It returns a pointer to the object that was allocated. new operator can also call the constructor of the object to initialize it.


**For example:**

```CPP
int* ptr = new int; // allocate memory for an integer
*ptr = 10; // store a value in the allocated memory

```

- delete operator is used to deallocate the memory that was allocated with new operator. It frees the memory back to the system for reuse. It is important to call delete on every pointer that was returned by new to avoid memory leaks.

**For example:**

```CPP
delete ptr; // deallocate the memory that was allocated with new

```
- It is worth noting that there is also an array form of new and delete operators for allocating and deallocating arrays of objects. For example:


```CPP
int* arr = new int[10]; // allocate memory for an array of 10 integers
delete[] arr; // deallocate the memory that was allocated with new[]

```

# new operator and operator new function are the same?

- No, new operator and operator new function are not the same

- new operator is used to dynamically allocate memory for an object and call its constructor to initialize it. It combines the functionality of operator new function and object initialization.

- operator new function is used to allocate memory, but it does not call the object constructor. It is called by the new operator to allocate memory for an object.

- Similarly, delete operator and operator delete function are used for deallocating memory for an object, where delete operator calls the object destructor before deallocating memory, whereas operator delete only deallocates memory.

# What is RAII idiom

- RAII stands for Resource Acquisition Is Initialization. It is an idiom in C++ that is used to manage resources such as memory, file handles, network connections, and other system resources.

- The basic idea of RAII is to associate the lifetime of a resource with the lifetime of an object, and to use the constructor and destructor of that object to manage the resource. The resource is acquired in the constructor, and released in the destructor, ensuring that it is released properly even in the presence of exceptions.

- For example, consider the case of dynamically allocated memory. Rather than using new and delete statements to allocate and deallocate memory directly, we can create a class that encapsulates the memory, and use its constructor and destructor to allocate and deallocate the memory. This ensures that the memory is properly released when the object goes out of scope, even in the presence of exceptions.

- RAII provides a way to manage resources in a safe and efficient manner, and is widely used in C++ programming.

# what is user declared - defined 

- In C++, a user-declared function is a function that has been declared in the program by the programmer, whereas a user-defined function is a function that has been both declared and defined by the programmer in the program.

- When a function is declared, the compiler is made aware of the function’s name, return type, and the number and types of its parameters. The definition of the function, on the other hand, provides the actual implementation of the function’s behavior.

**For example, consider the following code:*

```CPP
int add(int x, int y); // function declaration

int main() {
    int a = 5, b = 10;
    int sum = add(a, b); // function call
    return 0;
}

int add(int x, int y) { // function definition
    return x + y;
}

```
> In this code, add is a user-declared function because it is declared before it is used in the main function. However, it is also a user-defined function because it has a definition that provides the implementation of its behavior.


# what is user declared - defaulted

- In C++, user-declared defaulted functions are functions that are explicitly declared with the = default specifier. They are used to provide a default implementation of a function that the compiler can generate, but that the programmer wants to explicitly specify as the default.

**For example, consider a class with a default constructor:**

```CPP
class MyClass {
public:
    MyClass() = default;
};

```
> Here, the MyClass constructor is explicitly defined as defaulted using the = default specifier. This tells the compiler to generate a default implementation of the constructor, even though it has been explicitly defined.

- Similarly, user-declared deleted functions are functions that are explicitly declared as deleted using the = delete specifier. They are used to prevent the compiler from generating certain functions that would otherwise be generated automatically.

**For example, consider a class where copy constructor and copy assignment operator are deleted:**

```CPP
class MyClass {
public:
    MyClass() = default;
    MyClass(const MyClass&) = delete;
    MyClass& operator=(const MyClass&) = delete;
};

```

> Here, the copy constructor and copy assignment operator are explicitly deleted using the = delete specifier. This prevents the compiler from generating these functions, which would otherwise allow copying of the MyClass object.

# what is constructor initializer list

- Constructor initializer list is a special syntax in C++ used to initialize the member variables of a class inside the constructor of the class. It is used to set the initial value of the member variables of the class when an object is created, before the body of the constructor is executed.

- The constructor initializer list appears after the constructor prototype and before the opening curly brace of the constructor. It consists of a comma-separated list of member variable names, followed by their corresponding values enclosed in parentheses. For example:

```CPP
class MyClass {
public:
  MyClass(int a, int b) : x(a), y(b) {}
private:
  int x;
  int y;
};

```

> In this example, the constructor of MyClass takes two arguments, a and b, and initializes the member variables x and y using the constructor initializer list. This syntax can also be used to initialize non-static data members of class templates.

# what is non-static

- In C++, the keyword "non-static" is used to specify that a member variable or function is not shared among all instances of a class, but rather belongs to each individual instance of the class. Non-static members are also known as instance members or object members.

- Non-static member variables are declared inside a class but outside any member functions, and each instance of the class has its own copy of these variables. Non-static member functions are also declared inside a class and operate on the member variables of the class, but they are invoked on a specific instance of the class and can access the non-static member variables of that instance.

- In contrast, static members are shared among all instances of a class and are declared with the static keyword. They can be accessed without creating an instance of the class, and changes made to them affect all instances of the class.

# what is operator overloading

- Operator overloading in C++ is a technique that allows operators to be redefined or extended to work with user-defined data types, such as classes or structures. This means that operators such as +, -, *, /, =, ==, etc. can be overloaded to perform custom operations on objects of a class or structure.

- By overloading operators, C++ enables classes to behave like built-in data types, which makes the code more intuitive and easier to read. For example, overloading the + operator allows two objects to be added together with a syntax similar to the addition of integers, rather than using a method name like "Add" or "Sum".

# what are differences of copy constructor and copy assignment

- In C++, a copy constructor and a copy assignment operator are both used to copy objects. However, there are some differences between them:

1. **Copy constructor:** A copy constructor is a special constructor that is used to create a new object as a copy of an existing object. It is called when an object is initialized with another object of the same type. The copy constructor takes a reference to the object to be copied and creates a new object with the same values. It is used for creating a new object from an existing object.
2. **Copy assignment:** A copy assignment operator is a member function that is used to copy the values of one object to another object of the same type. It is called when an existing object is assigned a new value. The copy assignment operator takes a reference to the object to be copied and assigns the values to the new object. It is used for assigning a new value to an existing object.

- In summary, the main difference between a copy constructor and a copy assignment operator is that a copy constructor is used to create a new object from an existing object, while a copy assignment operator is used to assign a new value to an existing object.

# what is move semantics

- Move semantics in C++ is a feature introduced in C++11 to optimize the performance of object copies. When an object is copied, its data is duplicated to a new object, which can be expensive for large objects or when many copies are made. Move semantics allow objects to be "moved" from one location to another, without duplicating their data.

- In C++, move semantics are implemented using rvalue references, which allow objects to be bound to temporary values that are about to be destroyed. Move constructors and move assignment operators are defined using rvalue references to take advantage of this feature. When an object is moved, its data is simply transferred to the new object, rather than being duplicated.

- Move semantics are particularly useful for objects that manage large amounts of memory, such as containers or smart pointers. By allowing objects to be moved instead of copied, move semantics can greatly improve the performance of C++ programs.

# what move function is doing

- In C++, the std::move() function is used to indicate that an object can be moved from its current location to a new location without making a copy. This function is often used in conjunction with move constructors and move assignment operators to transfer ownership of resources from one object to another more efficiently than copying them.
- The std::move() function takes an rvalue reference to an object and returns an rvalue reference to that same object. It does not actually move the object itself, but rather converts it into an rvalue that can be used by move constructors and move assignment operators.

**For example, suppose we have a class MyClass that has a move constructor and a move assignment operator defined:**

```CPP
class MyClass {
public:
    // Move constructor
    MyClass(MyClass&& other) noexcept {
        // Move resources from other to this
    }

    // Move assignment operator
    MyClass& operator=(MyClass&& other) noexcept {
        // Move resources from other to this
        return *this;
    }
};

```

**We can use the std::move() function to transfer ownership of an object of MyClass from one location to another:**

```CPP
MyClass obj1;
// ...

MyClass obj2 = std::move(obj1);  // Uses move constructor
// ...

MyClass obj3;
// ...

obj3 = std::move(obj2);  // Uses move assignment operator

```

> In the example above, std::move(obj1) returns an rvalue reference to obj1, which is then used to construct obj2 using the move constructor. Similarly, std::move(obj2) returns an rvalue reference to obj2, which is then used to move-assign obj3.

# What is delegating constructor

- Delegating constructors are a feature introduced in C++11 that allows constructors to call other constructors within the same class. This can be useful when you have multiple constructors that share common initialization logic, so instead of duplicating the code in each constructor, you can delegate to a single constructor that performs the shared initialization.

- To use a delegating constructor, you simply call another constructor in the constructor initialization list, like this:

```CPP
class MyClass {
public:
    MyClass() : MyClass(0, 0) {} // delegating constructor

    MyClass(int a, int b) : x(a), y(b) {} // non-delegating constructor

private:
    int x, y;
};

```

> In this example, the default constructor delegates to the non-default constructor by calling MyClass(0, 0). This allows you to avoid duplicating the initialization logic in both constructors.

# What is conversion constructor

- In C++, a conversion constructor is a constructor that is used to implicitly convert one type to another. It is a type of constructor that accepts a single argument of a different type, allowing an object of one class to be created from an object of another class.


- For example, consider a class MyString that represents a string of characters. We can define a conversion constructor that takes a C-style string (a null-terminated array of characters) as input, and constructs a MyString object from it. The code for this conversion constructor might look like this:

```CPP
class MyString {
public:
    MyString(const char* str) {
        // implementation details
    }
};

```
> With this conversion constructor, we can create a MyString object from a C-style string as follows:

```CPP
const char* cstr = "hello world";
MyString mystr = cstr;  // implicitly convert C-style string to MyString object

```
> In this example, the conversion constructor allows us to create a MyString object from a C-style string without having to explicitly call the constructor.

# What is copy elision

- Copy elision is an optimization technique used by compilers in C++ to optimize the copy and move operations during function returns and variable initialization. It involves eliminating unnecessary copy and move operations by avoiding the creation of temporary objects.


- Copy elision occurs when the source object is constructed directly in the memory occupied by the target object. It allows the compiler to avoid creating a temporary object and then copying or moving its contents to the target object. This optimization can significantly improve performance and reduce memory usage in some cases.

- For example, consider the following code:

```CPP
#include <iostream>
#include <vector>

std::vector<int> createVector()
{
    std::vector<int> v{1, 2, 3, 4, 5};
    return v;
}

int main()
{
    std::vector<int> v1 = createVector();
    std::vector<int> v2{createVector()};
}

```
> In the above code, createVector() returns a std::vector<int> object. When we assign the result of createVector() to v1, a copy of the temporary object returned by createVector() is made. However, when we initialize v2 with createVector(), copy elision takes place, and no copy operation is performed.

- Copy elision is supported by all modern C++ compilers, and it is enabled by default at optimization levels -O1, -O2, and -O3. However, it is important to note that copy elision is not guaranteed by the C++ standard, and some cases may still require explicit use of move constructors and move assignment operators to achieve optimal performance.

# what is inline variable
























