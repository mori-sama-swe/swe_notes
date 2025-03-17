# Understanding Classes and Objects

## Classes: The Blueprint

A **class** in C++ is like a template or blueprint for creating objects. It defines:

- **Data** (attributes or properties, called *member variables*).
- **Behavior** (functions that operate on that data, called *member functions* or *methods*).

Think of a class as a custom data type you design yourself. For example, a Car class might describe what a car *has* (like speed or color) and what it *does* (like accelerate or stop).

## Objects: The Instances

> [!note]
>
> An **object** is an instance of a class—think of it as a real thing built from the blueprint. If Car is the class, then myCar or yourCar are objects. Each object gets its own copy of the class’s data but shares the same behavior (functions).

Example:

- **Class Definition**: class Car { ... }; defines the structure.

- **Objects**: myCar and yourCar are instances with their own brand and speed.

- **Dot Operator (. )**: Used to access members (e.g., myCar.brand or myCar.accelerate()).

```cpp
#include <iostream>
#include <string>

class Car {
public:  // Access specifier (more on this later)
    // Member variables (data)
    std::string brand;
    int speed;

    // Member function (behavior)
    void accelerate() {
        speed += 10;
        std::cout << brand << " is now at " << speed << " mph\n";
    }
};

int main() {
    // Creating objects
    Car myCar;          // Object 1
    Car yourCar;        // Object 2

    // Setting data
    myCar.brand = "Toyota";
    myCar.speed = 50;
    yourCar.brand = "Ford";
    yourCar.speed = 30;

    // Calling behavior
    myCar.accelerate();   // Outputs: Toyota is now at 60 mph
    yourCar.accelerate(); // Outputs: Ford is now at 40 mph

    return 0;
}
```

## Access Specifiers: Controlling Accessbility and Visibility 

> [!Note]
>
> Classes use **access specifiers** to decide who can touch their members:
>
> - **public**: Anyone can access these members.
> - **private**: Only the class itself can access them (default if you don’t specify).
>   - **Why**: private protects data, forcing you to use methods (like setters and getters) to change it safely.
> - **protected**: Like private, but also accessible to derived classes (more on inheritance later).

example:

```cpp
#include <iostream>
#include <string>

class Car {
private:  // Hidden from outside
    std::string brand;
    int speed;

public:   // Public interface
    void setBrand(std::string b) {
        brand = b;
    }
    void setSpeed(int s) {
        speed = s;
    }
    void accelerate() {
        speed += 10;
        std::cout << brand << " is now at " << speed << " mph\n";
    }
};

int main() {
    Car myCar;
    // myCar.brand = "Toyota";  // Error! brand is private
    myCar.setBrand("Toyota");   // Works via public method
    myCar.setSpeed(50);
    myCar.accelerate();         // Outputs: Toyota is now at 60 mph
    return 0;
}
```

## Constructors: Setting Up Objects

> [!important]
>
> A **constructor** is a special member function that runs when an object is created. It has the same name as the class and no return type. **Use it to initialize data.**
>
> - **Default Constructor**: If you don’t write one, C++ gives you a do-nothing default (e.g., Car()), but it’s gone once you define any constructor.

### Constructors: The Details

**Types of Constructors:**

> [!note]
>
> 1. **Default Constructor**
>
>    - Takes no parameters.
>
>    - Provided by C++ if you define no constructors; otherwise, you must write it.
>
>    - Initializes members to default values (e.g., 0 for ints, unless you specify otherwise).
>
>    ```cpp
>    #include <iostream>
>    
>    class Box {
>    public:
>        int width;
>        Box() {  // Default constructor
>            width = 10;
>            std::cout << "Default Box created\n";
>        }
>    };
>    
>    int main() {
>        Box b;  // Calls default constructor
>        std::cout << "Width: " << b.width << "\n";
>        return 0;
>    }
>    ```
>
> 2. **Parameterized Constructor**
>
>    - Takes arguments to initialize members with specific values.
>
>    - You can have multiple (overloaded) versions.
>
> ```cpp
> #include <iostream>
> 
> class Box {
> public:
>     int width;
>     Box(int w) {  // Parameterized constructor
>         width = w;
>         std::cout << "Box created with width " << w << "\n";
>     }
> };
> 
> int main() {
>     Box b(5);  // Calls parameterized constructor
>     std::cout << "Width: " << b.width << "\n";
>     return 0;
> }
> ```
>
> 3. **Copy Constructor**
>
>    - Creates a new object as a copy of an existing one.
>    - Default version does a shallow copy; you can define it for deep copying.
>
>    **Output**: Copied Box: Small.
>
>    **Why**: Without this, b2.name would point to b1.name, causing a double-delete crash.
>
>    ```cpp
>    #include <iostream>
>    #include <cstring>
>       
>    class Box {
>    public:
>        char* name;
>        Box(const char* n) {
>            name = new char[strlen(n) + 1];
>            strcpy(name, n);
>        }
>        Box(const Box& other) {  // Copy constructor
>            name = new char[strlen(other.name) + 1];
>            strcpy(name, other.name);
>            std::cout << "Copied Box: " << name << "\n";
>        }
>        ~Box() {
>            delete[] name;
>        }
>    };
>       
>    int main() {
>        Box b1("Small");
>        Box b2 = b1;  // Calls copy constructor
>        return 0;
>    }
>    ```
>
>    

### Move Constructor (C++ 11)

- Transfers resources from a temporary (rvalue) object to a new one, avoiding copies.

- `Uses && (rvalue reference).

```cpp
#include <iostream>
#include <utility>

class Box {
public:
    int* ptr;
    Box(int value) {
        ptr = new int(value);
        std::cout << "Created Box\n";
    }
    Box(Box&& other) noexcept : ptr(other.ptr) {  // Move constructor
        other.ptr = nullptr;
        std::cout << "Moved Box\n";
    }
    ~Box() {
        delete ptr;
    }
};

int main() {
    Box b1(42);
    Box b2(std::move(b1));  // Calls move constructor
    return 0;
}
```

### Overloading Constructors:

### What is Constructor Overloading?

> [!note]
>
> Constructor overloading is when a class has multiple constructors with the **same name** (the class name) but **different parameter lists**. Just like function overloading, the compiler picks the right constructor based on the number, types, or order of arguments you provide when creating an object.
>
> - **Why?** It gives flexibility: you can initialize an object in different ways depending on what data you have available.
> - **How?** Each constructor must have a unique signature (parameter list).
>
> **How Does It Work?**
>
> - Constructors are special member functions with no return type.
> - Overloading works by defining multiple versions, differing in:
>   - **Number of parameters**.
>   - **Types of parameters**.
>   - **Order of parameters**.
> - The compiler matches your object creation call (e.g., MyClass obj(arg1, arg2)) to the constructor with the best-fitting signature.

```cpp
#include <iostream>
#include <string>

class Box {
private:
    std::string name;
    int width;
    int height;

public:
    // Constructor 1: Default (no parameters)
    Box() {
        name = "Unknown";
        width = 0;
        height = 0;
        std::cout << "Default constructor\n";
    }

    // Constructor 2: One parameter (width only)
    Box(int w) {
        name = "Unknown";
        width = w;
        height = 0;
        std::cout << "Width-only constructor\n";
    }

    // Constructor 3: Two parameters (width and height)
    Box(int w, int h) {
        name = "Unknown";
        width = w;
        height = h;
        std::cout << "Width and height constructor\n";
    }

    // Constructor 4: All parameters (name, width, height)
    Box(std::string n, int w, int h) {
        name = n;
        width = w;
        height = h;
        std::cout << "Full constructor\n";
    }

    void display() {
        std::cout << "Box: " << name << ", " << width << "x" << height << "\n";
    }
};

int main() {
    Box b1;                  // Default
    Box b2(5);              // Width-only
    Box b3(5, 10);          // Width and height
    Box b4("Big", 20, 30);  // Full

    b1.display();
    b2.display();
    b3.display();
    b4.display();
    return 0;
}
```

### Constructor Initialization List (often called an "initializer list") 

In C++, a **constructor initialization list** (often called an "initializer list") is a <u>**way to initialize member variables of a class when an object is created.**</u> 

**It appears in the constructor definition and is placed after the constructor's parameter list, preceded by a colon (:)**. Using an initialization list is more efficient than assigning values inside the constructor body because it avoids double initialization of member variables.

basic syntax:

```cpp
ClassName::ClassName(parameters) : member1(value1), member2(value2), ... {
    // Constructor body (optional)
}
```

> [!note]
>
> **Key Points**
>
> 1. **Order of Initialization**: Members are initialized in the order they are declared in the class, not the order in the initialization list.
> 2. **Const Members**: Must be initialized in the initialization list because they cannot be assigned values after object creation.
> 3. **Reference Members**: Must also be initialized in the list since references cannot be reseated.
> 4. **Efficiency**: For non-primitive types (e.g., objects), the initialization list calls their constructors directly, avoiding default construction followed by assignment.

```cpp
#include <iostream>
#include <string>

class Person {
private:
    std::string name;       // Regular member
    const int age;          // Const member
    int& refToAge;          // Reference member

public:
    // Constructor with initialization list
    Person(std::string n, int a) : name(n), age(a), refToAge(age) {
        // No need to assign values here; initialization is already done
    }

    void display() const {
        std::cout << "Name: " << name << ", Age: " << age << std::endl;
    }
};

int main() {
    Person p("Alice", 25);
    p.display();
    return 0;
}
```

> [!important]
>
> **Explanation of the Example**
>
> - name(n): Initializes the name member with the string n.
> - age(a): Initializes the const int age with the value a.
> - refToAge(age): Initializes the reference refToAge to refer to age.
>
> **When to Use Initialization Lists**
>
> - **Mandatory**: For const members, references, and objects without default constructors.
> - **Recommended**: For better performance with non-primitive types (e.g., std::string, custom classes).

## Destructors: Cleaning Up

> [!important]
>
> A **destructor** runs when an object is destroyed (e.g., goes out of scope). It’s named ~ClassName() and has no parameters or return type. Useful for freeing resources (like memory).

example:

```cpp
#include <iostream>
#include <string>

class Car {
private:
    std::string brand;

public:
    Car(std::string b) {
        brand = b;
        std::cout << brand << " created\n";
    }
    ~Car() {
        std::cout << brand << " destroyed\n";
    }
};

int main() {
    Car myCar("BMW");  // Created here
    // Destroyed when main() ends
    return 0;
}
```

## Member Functions: Behavior Inside the Class

These are functions defined in the class to manipulate its data. You’ve seen accelerate() already. They can be defined inside or outside the class:

- `::` Ties the function to the Car class.

```cpp
class Car {
public:
    std::string brand;
    int speed;
    void accelerate();  // Declaration
};

void Car::accelerate() {  // Definition with scope resolution (::)
    speed += 10;
    std::cout << brand << " is now at " << speed << " mph\n";
}
```

## Passing Objects to Functions

Objects can be [passed by value (copy), reference (&), or pointer (*)](../cpp/c++ understanding functions.md#Passing by Value vs Passing By Reference)

example:

```cpp
#include <iostream>
#include <string>

class Car {
public:
    std::string brand;
    int speed;
};

void printCar(Car& c) {  // By reference, no copy
    std::cout << c.brand << " at " << c.speed << " mph\n";
}

int main() {
    Car myCar;
    myCar.brand = "Tesla";
    myCar.speed = 70;
    printCar(myCar);  // Outputs: Tesla at 70 mph
    return 0;
}
```

## Inheritance: Building on Classes

Inheritance lets one class (derived) inherit from another (base), reusing code.

> [!note]
>
> **What is Inheritance?**
>
> Inheritance allows a class (called the **derived class** or **child class**) to inherit properties and behaviors (member variables and functions) from another class (called the **base class** or **parent class**). 
>
> Think of it like a family tree: the child gets traits from the parent but can also add its own unique features or tweak what it inherits.

Basic Syntax:

- **access_specifier**: Usually public, but can be private or protected (more on this soon).

  The colon (:) says, “Derived inherits from Base.”

```cpp
class Base {
    // Base class stuff
};

class Derived : access_specifier Base {
    // Derived class stuff
};
```

Example:

- **What’s happening**:
  - Car inherits type, speed, and move() from Vehicle.
  - Car adds its own accelerate() method.

```cpp
#include <iostream>
#include <string>

class Vehicle {  // Base class
public:
    std::string type;
    int speed;

    void move() {
        std::cout << type << " is moving at " << speed << " mph\n";
    }
};

class Car : public Vehicle {  // Derived class
public:
    void accelerate() {
        speed += 10;
        std::cout << "Car accelerated to " << speed << " mph\n";
    }
};

int main() {
    Car myCar;
    myCar.type = "Sedan";  // From Vehicle
    myCar.speed = 50;      // From Vehicle
    myCar.move();          // From Vehicle: Sedan is moving at 50 mph
    myCar.accelerate();    // From Car: Car accelerated to 60 mph
    return 0;
}
```

### Access Specifiers in Inheritance

The **access specifier** in the inheritance declaration (public, private, protected) controls how the base class’s members are inherited. Here’s the breakdown:

> [!important]
>
> 1. **public Inheritance**
>
>     (Most Common)
>
>    - Public members stay public.
>    - Protected members stay protected.
>    - Private members are inaccessible directly (but still there, usable via base class methods).
>    - **Meaning**: The derived class keeps the base class’s interface open to the outside world.
>
> 2. **protected Inheritance**
>
>    - Public and protected members become protected in the derived class.
>    - Private members remain inaccessible.
>    - **Meaning**: Hides the base class’s public stuff from the outside, but derived classes can still use it internally.
>
> 3. **private Inheritance**
>
>    - All base class members (public and protected) become private in the derived class.
>    - Private members stay inaccessible.
>    - **Meaning**: Locks everything down—only the derived class can use the base class’s stuff, not even further descendants.

Example:

```cpp
#include <iostream>

class Base {
public:
    int publicVar = 1;
protected:
    int protectedVar = 2;
private:
    int privateVar = 3;
};

class PublicDerived : public Base {
public:
    void show() {
        std::cout << "Public: " << publicVar << ", Protected: " << protectedVar << "\n";
        // privateVar inaccessible here
    }
};

class ProtectedDerived : protected Base {
public:
    void show() {
        std::cout << "Protected: " << publicVar << ", " << protectedVar << "\n";
    }
};

int main() {
    PublicDerived pub;
    std::cout << pub.publicVar << "\n";  // OK: 1
    pub.show();                          // Public: 1, Protected: 2

    ProtectedDerived prot;
    // std::cout << prot.publicVar;  // Error: publicVar is protected now
    prot.show();                    // Protected: 1, 2
    return 0;
}
```

### Constructors and Destructors in Inheritance

- **Constructors**: Base class constructor runs first, then derived class constructor.
- **Destructors**: Derived class destructor runs first, then base class destructor (opposite order).

```cpp
#include <iostream>
#include <string>

class Vehicle {
public:
    std::string type;
    Vehicle(std::string t) : type(t) {
        std::cout << "Vehicle created: " << type << "\n";
    }
    ~Vehicle() {
        std::cout << "Vehicle destroyed: " << type << "\n";
    }
};

class Car : public Vehicle {
public:
    int speed;
    Car(std::string t, int s) : Vehicle(t), speed(s) {
        std::cout << "Car created with speed " << speed << "\n";
    }
    ~Car() {
        std::cout << "Car destroyed\n";
    }
};

int main() {
    Car myCar("SUV", 60);
    return 0;
}
```

### Types of Inheritance

1. **Single Inheritance**: One base class, one derived class (like all examples so far).
2. **Multiple Inheritance**: A class inherits from more than one base class.

```cpp
class Engine {
public:
    void start() { std::cout << "Engine started\n"; }
};
class Body {
public:
    void honk() { std::cout << "Beep!\n"; }
};
class Car : public Engine, public Body {
public:
    void drive() { std::cout << "Driving\n"; }
};
int main() {
    Car myCar;
    myCar.start();  // From Engine
    myCar.honk();   // From Body
    myCar.drive();  // From Car
    return 0;
}
```

> [!note]
>
> **Wrap-Up**
>
> - **Inheritance** builds hierarchies: base classes provide shared stuff, derived classes specialize.
> - **Access** (public, etc.) shapes how members are inherited.
> - **Constructors/Destructors** chain up and down the hierarchy.
> - **Types** like multiple or multilevel add flexibility but complexity (e.g., diamond problem).
> - **Overriding** lets derived classes customize behavior.

## Polymorphism

## Virtual Functions



