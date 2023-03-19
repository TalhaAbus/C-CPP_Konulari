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
> In the above code, createVector() returns a std::vector<int object. When we assign the result of createVector() to v1, a copy of the temporary object returned by createVector() is made. However, when we initialize v2 with createVector(), copy elision takes place, and no copy operation is performed.

- Copy elision is supported by all modern C++ compilers, and it is enabled by default at optimization levels -O1, -O2, and -O3. However, it is important to note that copy elision is not guaranteed by the C++ standard, and some cases may still require explicit use of move constructors and move assignment operators to achieve optimal performance.




# what is inline variable

- In C++, an inline variable is a variable declared with the inline keyword. It instructs the compiler to replace all the references to the variable with its actual value, similar to an inline function. This can result in improved performance and smaller code size, as it avoids the overhead of a function call or a variable lookup.

- Inline variables were introduced in C++17 and can be used to declare both static and non-static data members of a class. An inline variable must have a definition in the header file, and it can be initialized using an initializer or default initialization.

- Here's an example of an inline variable declaration:

```CPP
// header file

class MyClass {
public:
    inline static int myInt = 42;   // an inline static data member
    inline float myFloat;           // an inline non-static data member

    MyClass() : myFloat(3.14f) {}   // constructor definition
};

// source file

int main() {
    MyClass obj;
    int result = MyClass::myInt * obj.myFloat;  // the reference to myInt and myFloat is replaced with their actual values
    return 0;
}

```

# what is friend keyword

- In C++, the friend keyword is used to grant access to private or protected class members to functions or classes that are not members of the class. When a function or a class is declared as a friend of a class, it is given permission to access the private and protected members of the class as if they were its own members.

- The friend keyword is often used when implementing operator overloading in C++, allowing non-member functions to have access to private and protected members of a class. It can also be used when implementing the Pimpl idiom, where a class exposes only its public interface and hides its implementation details in a separate class that is declared as a friend of the public class.

- It is worth noting that using the friend keyword can potentially compromise the encapsulation and data hiding features of object-oriented programming, so it should be used judiciously and only when necessary.

# what is Pimpl idiom

- Pimpl (Pointer to implementation) is an idiom in C++ used for implementing the opaque pointer pattern. The main idea is to separate the implementation of a class from its interface by hiding the details of the implementation in a separate class or structure. This can make it easier to change the implementation of a class without affecting the code that uses it.

- In Pimpl idiom, the public interface of a class contains only the member function declarations, and the private implementation details are hidden behind a pointer to an implementation class. The implementation class is defined in the .cpp file, and its members are not visible to the client code. This way, any changes made to the implementation class will not require recompiling the client code.
- Pimpl idiom also allows for greater encapsulation, as it enables hiding the private members and functions of a class from its users. This can be useful when working with complex classes that have a lot of private data and functions.

# what is friend keyword

- In C++, the friend keyword is used to grant access to private or protected members of a class to another class or function. When a function or class is declared as a friend of a class, it can access the private and protected members of that class, as if they were its own members. This allows for more flexible and granular control over access to a class's data and methods, while still allowing selected external entities to manipulate its state.

- It's worth noting that using friend can break encapsulation and make code harder to maintain, so it should be used judiciously and with care.

# what is operator overloading

- Operator overloading in C++ allows you to define the behavior of operators (+, -, *, /, etc.) when they are used with user-defined types (classes or structures). With operator overloading, you can use operators on objects just like you do with built-in data types like integers and floating-point numbers.

- For example, you can overload the '+' operator to allow addition of two objects of a custom class. Here's an example:

```CPP
class Vector {
public:
    Vector operator+(const Vector& other) const {
        Vector result;
        result.x = x + other.x;
        result.y = y + other.y;
        return result;
    }

private:
    int x, y;
};

int main() {
    Vector v1 = { 1, 2 };
    Vector v2 = { 3, 4 };
    Vector v3 = v1 + v2; // calls the overloaded '+' operator
}

```
> In this example, the operator+ function is overloaded for the Vector class, allowing you to use the + operator to add two Vector objects together.


# Why operator overloading is exist

- Operator overloading exists in C++ to allow programmers to use the built-in operators such as +, -, *, /, etc. to work with user-defined types, just as they work with fundamental types like integers and floating-point numbers. This makes the code more readable and intuitive. For example, if we have a class that represents a complex number, we can overload the + operator so that we can add two complex numbers using the same syntax as we use for adding two integers.


- In addition, operator overloading can also improve the performance of code in some cases by allowing the compiler to generate more optimized code for a particular operation.

# How can we add two complex numbers if operator overloading is not exist

```CPP
#include <iostream>

struct Complex {
    double real, imag;

    Complex(double real, double imag) : real(real), imag(imag) {}

    friend Complex add(const Complex& c1, const Complex& c2) {
        return Complex(c1.real + c2.real, c1.imag + c2.imag);
    }
};

int main() {
    Complex c1(1.0, 2.0);
    Complex c2(2.0, 3.0);

    Complex c3 = add(c1, c2);

    std::cout << "c1 + c2 = " << c3.real << " + " << c3.imag << "i" << std::endl;

    return 0;
}

```

> As you can see, we have defined a add() function that takes two Complex objects as arguments and returns a Complex object that is the sum of the two input objects. In the main() function, we use this function to add two complex numbers.

# what is user defined conversion
- User-defined conversions in C++ allow you to define custom type conversions between types. These conversions can be implicitly or explicitly invoked.

- There are two types of user-defined conversions in C++:

1. **Conversion constructors:** These are constructors that can accept a single argument and are used to convert one type to another.

- Here's an example of a conversion constructor that converts a double to an integer:


```CPP
class MyInt {
public:
    MyInt(double d) {
        value = static_cast<int>(d);
    }
private:
    int value;
};

```
- With this conversion constructor, you can create an instance of MyInt from a double:


```CPP
MyInt myint = 3.14;

```

- **Conversion operators:** These are member functions that allow you to convert an object of one class to another class.

- Here's an example of a conversion operator that converts a MyInt object to an int:


```CPP
class MyInt {
public:
    operator int() const {
        return value;
    }
private:
    int value;
};

```

- With this conversion operator, you can convert a MyInt object to an int:


```CPP
MyInt myint(42);
int i = myint;

```

# how to convert a class type object with user defined conversion

- To convert a class type object using user-defined conversion, you need to define a conversion function in your class. The conversion function should have the following properties:

- It must be a member function of the class you want to convert from
- It must not have a return type, but it should return a value of the desired type
- It should not take any arguments, except possibly for a const reference to the current object

**Here's an example of a class with a conversion function that converts the object to an integer:**


```CPP
class MyClass {
public:
  operator int() const {
    return myInt;
  }

private:
  int myInt;
};

```
> In this example, the operator int() function is the conversion function. It takes no arguments and returns an integer, which is the type that we want to convert to. Inside the function, we simply return the value of myInt, which is a member variable of the class.

- Once you've defined the conversion function, you can use it to convert objects of your class to the desired type. For example:

```CPP
MyClass obj;
int i = obj;  // convert obj to an int using the conversion function

```

> In this example, obj is an object of type MyClass, but we're able to assign it to an int variable i because the conversion function allows us to convert a MyClass object to an int.


# what is conversion operator

- A conversion operator is a special member function in C++ that enables a class to convert to a specified type. It allows the class to be used in expressions where the target type is expected, by implicitly converting the object to that type.

- In other words, a conversion operator defines a way for a user-defined class to be implicitly converted to another type. The syntax for defining a conversion operator is as follows:


```CPP
operator type() const;

```

- Here, type is the type to which the class should be converted. The const qualifier at the end of the function declaration indicates that the function will not modify the object being converted.

- Conversion operators can be useful in situations where you want to use your own class types with other library functions or operators that expect built-in types. For example, you might define a class to represent a physical quantity, such as length or mass, and use a conversion operator to convert the object to a built-in type like double. This would allow you to perform arithmetic operations with the physical quantity class using the same syntax as for built-in types.

# what is unique_ptr

- std::unique_ptr is a smart pointer provided by the C++ Standard Library that provides automatic memory management for dynamically allocated objects. It is used to manage resources that need to be deallocated explicitly, such as dynamically allocated objects or resources acquired from an operating system call.

- A unique_ptr is unique in the sense that it is the sole owner of the pointer it manages, meaning there is no other pointer pointing to the same memory. When a unique_ptr is destroyed, it automatically releases the memory it owns, thereby avoiding memory leaks.

- unique_ptr is implemented as a template class that wraps a pointer to an object and provides a set of member functions to manage that object. It is non-copyable but can be moved, which means that ownership of the underlying resource can be transferred to another unique_ptr.

- Here is an example of using unique_ptr to manage a dynamically allocated object:


```CPP
#include <memory>
#include <iostream>

int main() {
    std::unique_ptr<int> myInt(new int(42));
    std::cout << "myInt points to " << *myInt << std::endl;
    // when myInt goes out of scope, it will automatically release the memory it owns
    return 0;
}

```

# is unique_ptr can be moved only to an other unique_ptr

- No, a unique_ptr can also be moved to an std::shared_ptr or an std::weak_ptr. However, moving a unique_ptr to any other type of pointer is not allowed and will result in a compiler error. The reason for this is that the unique ownership semantics of a unique_ptr are not compatible with shared ownership semantics of std::shared_ptr or raw pointers.

# what are the namespaces of standart library std

- The standard library of C++ defines many functions and types in the std namespace. Some of the commonly used namespaces in the standard library include:


- std::chrono: for time-related utilities
- std::filesystem: for file and directory operations
- std::iostreams: for input and output streams
- std::algorithm: for algorithms such as sorting, searching, etc.
- std::string: for string operations
- std::vector: for dynamic arrays
- std::map: for key-value mappings
- std::set: for sets of unique elements
- std::thread: for multithreading
- And many more.

# what is "cout"

- cout is an object of the std::ostream class in the std namespace. It is used to output data to the console or other output streams. It is commonly used in C++ programs to display the results of a program or to provide information to the user. The std::cout object is defined in the <iostream header file, which is part of the C++ standard library.

# How "cout" object output data to the console

- In C++, the cout object is an instance of the ostream class, which is defined in the <iostream header. The ostream class provides methods for outputting formatted data to various output devices, including the console. When you call the << operator on the cout object, you are actually calling the operator<< method of the ostream class, passing in the data that you want to output as a parameter. The operator<< method then writes the data to the console using various formatting options, such as padding and precision.

# what is "using" decleration

- In C++, using declaration is used to introduce a symbol or a namespace into the current scope, to avoid typing the full qualified name every time it is used.

- For example, if you have a long namespace name like std::chrono::high_resolution_clock, you can use using declaration to introduce the namespace and avoid typing the full name every time you want to use it:

```CPP
#include <chrono>
using std::chrono::high_resolution_clock;

int main() {
    auto t1 = high_resolution_clock::now();
    // ...
}

```

- In this example, using std::chrono::high_resolution_clock introduced 
- high_resolution_clock into the current scope, so we can use 
- high_resolution_clock::now() instead of 
- std::chrono::high_resolution_clock::now().

# what is "using namespace" decleration and what are differences with "using" decleration


- In C++, a using directive is used to bring all the declarations of a namespace into the current scope. The syntax for using directive is using namespace name_of_namespace;.


**For example:**
```CPP
#include <iostream>

using namespace std;

int main()
{
    cout << "Hello, World!" << endl;
    return 0;
}

```

- Here, using namespace std; brings all the declarations of the std namespace into the current scope. So, we can use cout directly instead of qualifying it with std::.

- A using declaration, on the other hand, is used to bring a specific declaration from a namespace into the current scope. The syntax for using declaration is using name_of_namespace::name_of_declaration;.

**For example:**

```CPP
#include <iostream>

using std::cout;

int main()
{
    cout << "Hello, World!" << std::endl;
    return 0;
}

```
> Here, using std::cout; brings the cout declaration from the std namespace into the current scope. So, we can use cout directly instead of qualifying it with std::. However, other declarations from the std namespace are not brought into the current scope.

# What is ADL (Argument dependant lookup)

- Argument-dependent lookup (ADL), also known as argument-dependent name lookup or Koenig lookup, is a feature of C++ that allows functions and operators to be overloaded based on the types of arguments passed to them. When a function or operator is called with arguments of a certain type, the compiler will look for its definition not only in the current scope, but also in the namespaces associated with those argument types.

- For example, suppose we have a function print and a type my_type defined in the namespace my_ns:

```CPP
namespace my_ns {
    struct my_type {};
    void print(my_type const& x) {
        // ...
    }
}

```


- If we call print with an argument of type my_type, we can omit the namespace qualification for the function:

```CPP
my_ns::my_type x;
print(x); // uses my_ns::print

```
- This is because the compiler will look for print in the my_ns namespace due to the type of x being my_type. ADL can be useful for writing more generic code that can work with types from different namespaces. However, it can also sometimes cause unexpected overloading or name resolution, so it is important to be aware of its behavior when writing C++ code.

# what is unnamed namespace

- In C++, an unnamed namespace is a namespace without a name that is used to declare variables, functions, and classes that are only accessible within a single translation unit. When you define an unnamed namespace, the contents of the namespace are only visible within the file in which they are defined, and they are not accessible from other files.


- For example, consider the following code snippet:

```CPP
// foo.cpp
namespace {
    int x = 42;
}

void foo() {
    x = 24; // x is visible only within foo.cpp
}

```
> In this code, an unnamed namespace is used to define an integer variable x. Since the namespace is unnamed, its contents are only visible within foo.cpp, and x cannot be accessed from other translation units. This provides a way to encapsulate implementation details within a file and avoid naming collisions with other files.

# So it's kind of like getting the variables in the file scope right?
- Yes, that's correct. The variables declared in an unnamed namespace have file scope, but they are only accessible within the translation unit in which they are defined. This allows you to declare variables that are private to a particular source file and not visible to the rest of the program.

# what is inline namespace

- An inline namespace is a C++11 feature that allows you to define a namespace that is a member of another namespace or of a class, and whose members are automatically brought into the enclosing namespace or class scope, as if the inline namespace was part of the enclosing scope.

- In other words, an inline namespace allows you to define a group of related symbols, but without introducing an additional level of nesting. This can be useful when you want to version your interfaces or organize your code in a more modular way.

- Here's an example of how to use an inline namespace:

```CPP
namespace my_library {
    inline namespace v1 {
        void my_function() {
            std::cout << "Hello from version 1\n";
        }
    }

    inline namespace v2 {
        void my_function() {
            std::cout << "Hello from version 2\n";
        }
    }
}

int main() {
    my_library::my_function();  // Calls the function from v2
    return 0;
}

```

- In this example, we define an inline namespace v1 and v2 inside the my_library namespace. The my_function() is defined in both namespaces. When we call my_function() inside main(), it will call the version of my_function() that is defined in the latest inline namespace (v2 in this case), since it overrides any definitions in earlier inline namespaces.

# why inline namespaces exist?

- Inline namespaces in C++ exist to allow for more flexible versioning and extension of code.
- Suppose you have a library or module that provides some functionality, and you want to extend it or modify it while still maintaining backwards compatibility for existing code that uses the original version of the library. You could achieve this by creating a new namespace for the modified version of the library, but then you would have to update all the code that uses the original version of the library to use the new namespace. This can be a lot of work and can introduce bugs if the update is not done carefully.
- Instead, you can use an inline namespace to create a new version of the library that is nested within the original namespace. Code that uses the original version of the library can continue to use the original namespace, while code that uses the new version can use the nested inline namespace. This way, both versions of the library can coexist in the same program without conflict.
- Furthermore, because the new version of the library is an inline namespace, any code that depends on the original version of the library will automatically pick up the new version if it is available, without needing to be updated. This makes it easy to extend and modify existing code without introducing breaking changes.


# what is namespace alias
- Namespace alias is a feature in C++ that allows creating an alias or alternative name for an existing namespace. It provides a way to refer to a namespace with a different name, making it easier to use in code.

- Namespace alias is created using the namespace keyword followed by the new name and the = operator, followed by the original namespace name. For example, the following code creates an alias for the std namespace:

```CPP
namespace new_name = std;

```
- After this declaration, you can use new_name instead of std in your code. This is useful when you want to shorten long namespace names, create a more descriptive name, or when you want to avoid namespace conflicts.

- Namespace alias can be declared at global scope, function scope, or block scope, and can be used with any namespace.

# what is nested type

- In C++, a nested type is a type that is defined inside another type. For example, a class can have a nested class, and a struct can have a nested enum. The nested type is then considered a member of the enclosing type and can be accessed using the scope resolution operator ::.

- Here's an example of a nested class:


```CPP
class Outer {
public:
    class Inner {
    public:
        void foo();
    };
};

void Outer::Inner::foo() {
    // ...
}

int main() {
    Outer::Inner obj;
    obj.foo();
}

```
> In this example, Inner is a nested class of Outer. The foo() function of the nested class is defined outside the class definition using the scope resolution operator ::. To create an object of the nested class, we use the scope resolution operator to specify the enclosing class, like Outer::Inner obj;.

# can a nested type access to the private section

- Yes, a nested type can access the private section of its enclosing class. Since a nested type is a member of its enclosing class, it has access to all members (including private members) of its enclosing class.

- However, it is important to note that the nested type itself may have different access control restrictions depending on how it is declared. For example, a nested class declared as "private" can only be accessed by its enclosing class and its friends.

# what is containment

- Containment in C++ is a way of creating a class by including one or more objects of other classes as member variables of the new class. It is also known as composition.

- In containment, a class contains one or more objects of other classes as its member variables. These member variables can be used to provide additional functionality to the class, or to represent relationships between different objects.

- Containment is an important concept in object-oriented programming because it allows for the creation of complex classes and relationships between objects. It is often used to model real-world relationships between objects, such as a car containing an engine and a transmission, or a company containing multiple departments.

# Association - Aggregation - Composition ?

- In object-oriented programming, there are three types of relationships between classes: Association, Aggregation, and Composition.

- **Association** represents a relationship between two classes, where each class has its own life cycle and there is no ownership between them. For example, a teacher and a student can have an association where a teacher teaches a student. But, the student is not owned by the teacher, and the student can exist without the teacher.

- **Aggregation** is a type of association where one class owns another class, and the owned class cannot exist without the owner. However, the owned class has its own life cycle, and it can belong to multiple owners. For example, a car can have an aggregation relationship with its engine. The car owns the engine, and the engine cannot exist without the car. But, the engine can also be used in other cars.

- **Composition** is also a type of association where one class owns another class, but the owned class cannot exist without the owner. The difference between aggregation and composition is that in composition, the owned class is part of the owner class, and it cannot be shared with other owners. For example, a car can have a composition relationship with its tires. The tires are part of the car, and they cannot be used by other cars.

# what is STL

- STL stands for Standard Template Library, which is a library of reusable code components in C++ programming language. The library provides a set of container classes, algorithms, and iterators that are implemented using templates. The templates allow for generic programming, which means that the same code can be used for different types of data.

- The container classes in STL include vector, list, deque, map, set, and others. These containers provide a way to store and organize data in memory. Algorithms in the library include sorting, searching, and other operations that can be performed on containers. Iterators provide a way to access and manipulate data in containers in a flexible way.

- STL is part of the C++ Standard Library and is widely used in C++ programming for its efficiency and flexibility. It has become an essential tool for C++ developers and is often used in software development projects that require efficient data structures and algorithms.

# Is that a generic library ? What kind of things exist in STL library?

- Yes, the STL (Standard Template Library) is a generic library that provides a collection of powerful and efficient algorithms and data structures. The STL is a part of the C++ standard library and it provides a framework for implementing container classes, iterators, algorithms, and function objects.


- The STL library includes several container classes such as vectors, lists, maps, sets, and queues. It also includes several algorithms such as sorting, searching, and transforming that can be used with these containers. Additionally, the STL provides several iterator types that allow for traversal of container elements and algorithms.

- Some other features of the STL include function objects, which are objects that behave like functions, and smart pointers such as unique_ptr and shared_ptr, which are used for automatic memory management. Overall, the STL provides a powerful set of tools for developers to use when building C++ applications.

# Can you elaborate on "function objects" ?

- Function objects, also known as functor, are objects that can be used as functions. In C++, a function object is a class type that overloads the function call operator operator() and can be invoked like a function.

- Unlike regular functions, function objects can have state, allowing them to keep track of data across multiple calls. They can also be customized to perform specific operations, making them powerful tools for data processing and manipulation.

- Function objects are widely used in the STL, where they are often used as predicates for algorithms like sort() or find_if(). They are also used as custom comparators for containers like set and map.


- Here is an example of a function object that calculates the sum of two integers:

```CPP
class Adder {
public:
    int operator()(int x, int y) {
        return x + y;
    }
};

int main() {
    Adder add;
    int sum = add(2, 3); // sum is 5
}

```
> In this example, Adder is a function object that overloads the operator() to perform the addition of two integers. The object add can be called like a function to calculate the sum of two numbers.

# what is dynamic array

- A dynamic array, also called a resizable array or a dynamic array container, is an array-like data structure that can change its size dynamically during runtime. In contrast to a static array, where the size is fixed and determined at compile time, the size of a dynamic array can be increased or decreased at runtime as needed. This flexibility makes dynamic arrays a popular choice for many programming tasks, particularly when dealing with large amounts of data.

- In C++, the standard library provides a dynamic array container called std::vector. The std::vector class encapsulates a dynamic array and provides a variety of methods to manipulate the array, such as adding or removing elements, accessing elements by index, and changing the size of the array. Dynamic arrays are often implemented using a combination of memory allocation and copying operations behind the scenes to ensure efficient resizing and memory management.

# How does dynamic arrays work?

- In C++, dynamic arrays are created using pointers and allocated in the heap memory. When a dynamic array is created, the program requests a block of memory from the operating system using the new operator. The amount of memory requested is based on the number of elements that the dynamic array will store, and the size of each element.
- For example, if we want to create an array of 10 integers, we would use the following code:

```CPP
int* arr = new int[10];

```
- This code creates a dynamic array of 10 integers and returns a pointer to the first element of the array, which is stored in the arr variable.

- To access an element in the dynamic array, we use the array indexing operator []. For example, to set the value of the first element in the array to 42, we would use the following code:

```CPP
arr[0] = 42;

```
- When we are finished using the dynamic array, we need to free the memory that was allocated using the delete[] operator. For example:

```CPP
delete[] arr;

```
- This releases the memory that was allocated for the dynamic array back to the operating system.

- It's important to note that when using dynamic arrays, we are responsible for managing the memory ourselves. This means that we need to make sure that we delete the array when we are finished using it to avoid memory leaks. Additionally, we should be careful not to access memory that has already been freed, as this can result in undefined behavior.

# How much storage does it occupy in memory ? What kind of pointers does it contain?

- The amount of memory occupied by a dynamic array depends on the number of elements it contains and the size of each element. The total size of the array can be calculated as number_of_elements * size_of_each_element

- Dynamic arrays are usually allocated using the new operator, which returns a pointer to the first element of the array. The pointer is of the same type as the elements of the array, so if the array contains int elements, the pointer will be of type int*.

- The pointer returned by new points to a block of contiguous memory that can be accessed using array syntax, e.g. array[0], array[1], etc. Since the pointer points to the first element of the array, it can be used to access any element by adding an offset to the pointer.

- It's important to note that dynamic arrays don't have any built-in bounds checking, so it's the responsibility of the programmer to ensure that array indices are within the bounds of the array.


# What are the 3 pointers held by dynamic arrays?

- Dynamic arrays in C++ are allocated from the heap using the new keyword and they return a pointer to the first element of the array. There is only one pointer that points to the start of the array, but it is possible to access other elements in the array by incrementing or decrementing the pointer.

- In addition to the pointer to the start of the array, there are two other pointers held by dynamic arrays:

1. A pointer to the end of the allocated memory. This pointer is often called the "past-the-end" pointer or "one-past-the-end" pointer and points to the memory location immediately following the last element of the array.
2. A pointer to the size of the allocated memory. This pointer is often called the "size" pointer and contains the number of elements that have been allocated for the array.

# is string a template ? what is basic_string ? 

- std::string is a typedef for a specialization of the std::basic_string class template in the C++ Standard Library.

- std::basic_string is a class template that provides a mechanism to store and manipulate sequences of characters in C++. It is parameterized by a character type (such as char or wchar_t), an allocator type, and other optional template parameters.

- In other words, std::string is a specific instantiation of std::basic_string with the character type set to char. It provides a convenient way to work with strings of characters in C++, including support for many common string operations such as concatenation, substring extraction, and searching.

# what is SSO (Small string optimization

- SSO (Small String Optimization) is a technique used in some C++ standard library implementations to optimize the storage of small strings. The basic idea is to avoid allocating dynamic memory on the heap for small strings, and instead store the string directly in the memory of the string object itself.

- In the case of std::string, SSO means that if the string is small enough (typically 15 characters or less), the characters will be stored directly in the string object itself, rather than being allocated on the heap. This can result in significant performance improvements for small strings, since heap allocation and deallocation can be relatively expensive.

- If the string grows beyond the SSO limit, then dynamic memory will be allocated on the heap to store the additional characters. This means that the std::string object will contain both the small string buffer and the heap-allocated buffer.

- Note that SSO is an implementation detail, and is not required by the C++ standard. Some implementations may not use SSO at all, while others may use different thresholds for determining when to use SSO.

# What is a container ? Is string a container ?

- In programming, a container is a data structure that is used to store and organize other objects or elements of data. Containers can be used for a variety of purposes, such as managing collections of data or implementing algorithms and data structures.

- In C++, the Standard Template Library (STL) provides a variety of container classes that can be used to store data. These container classes include vector, list, map, set, and others.

- String is also a container in C++. It is a container class that represents a sequence of characters. It is based on the basic_string template class, which provides a general implementation of a string class that can be used with a wide range of character types.

- In computer science, a container is an object that can store and organize other objects or data. A container can be thought of as a way to hold and manage a collection of objects or data, providing various operations for adding, removing, and manipulating the elements within it.

- In the context of C++, the Standard Template Library (STL) provides several container classes that are implemented as template classes. These container classes include vector, list, map, set, and others. These containers are designed to hold elements of various types, such as integers, strings, or user-defined objects, and provide a range of operations for managing and manipulating the contained elements.

- Each container has its own characteristics and trade-offs in terms of storage, access speed, insertion and deletion speed, and other factors. Choosing the appropriate container for a particular task depends on the requirements of the task and the performance characteristics of the container.

- As for string, yes, it can be considered a container in the sense that it is an object that can hold and manage a sequence of characters. More specifically, string is a container class that is implemented as a specialization of the basic_string template class in the STL.

# how to use containers

- To use containers, you first need to include the appropriate header file. For example, to use std::vector, you would include the <vector header:
                                                                                                                                           
              
                                                                                                                        
```CPP
#include <vector>

int main() {
    // create a vector of integers
    std::vector<int> vec = {1, 2, 3, 4, 5};

    // add an element to the vector
    vec.push_back(6);

    // iterate over the elements of the vector and print them
    for (auto it = vec.begin(); it != vec.end(); ++it) {
        std::cout << *it << " ";
    }

    return 0;
}

    
```
> This example creates a std::vectorint object named vec, initializes it with five integers, adds a sixth integer to the end of the vector using the push_back() function, and then iterates over the elements of the vector using a for loop and prints them to the console.

- You can use other containers in a similar way, but with different functions and iterators specific to each container

# what is iterator

    
  
                                         
- In C++, an iterator is an object that allows iteration (looping) through a container of elements, like an array or a standard container like vector, set, map, etc. Iterators are used to traverse the elements of a container and access them. They act as a generalization of pointers and allow generic algorithms to be written that can work with different types of containers.

- Iterators can be classified into different types based on the level of access they provide to the underlying container. Some of the common types of iterators are:

1. **Input iterators:** These iterators provide read-only access to a container and allow iteration over its elements in a forward-only direction.

2. Output iterators: These iterators provide write-only access to a container and allow iteration over its elements in a forward-only direction.
                                         
                                         
                                         
                                       
















