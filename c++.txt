Here is a comprehensive set of questions for the topic of **OOP (Object-Oriented Programming)** in C++, following your requested format.

-----

### \#\# 1. Coding Questions

  * **Easy (1 Question)**

    1.  Create a `class` named `Car` with two `private` member variables: `brand` (a `std::string`) and `year` (an `int`). Implement a constructor to initialize these members and a `public` member function `display()` that prints "This is a [year] [brand]."

  * **Medium (5 Questions)**

    1.  Create a base class `Animal` with a `public` function `eat()`. Create a derived class `Dog` that inherits from `Animal` and has its own `public` function `bark()`. In `main`, create a `Dog` object and call both `eat()` and `bark()`.
    2.  Modify your `Car` class to include a `static` member variable `objectCount`. This variable should be incremented every time a new `Car` object is created. Write a `static` function `getCount()` that returns the total count.
    3.  Create a `Book` class. Overload the `==` operator so that two `Book` objects are considered equal if their `isbn` (a `std::string` member) is the same.
    4.  Implement a class `Rectangle` with `private` members `width` and `height`. Write a `const` member function named `getArea()` that returns the area. In `main`, create a `const Rectangle` object and call `getArea()`.
    5.  Implement a `Student` class. Write a member function `setAge(int age)` that uses the `this` pointer to distinguish between the member variable `age` and the parameter `age`.

  * **Hard (3G Questions)**

    1.  Design a class hierarchy to demonstrate polymorphism. Create an abstract base class `Shape` with a pure virtual function `virtual double area() = 0;`. Derive two classes, `Circle` and `Square`, from `Shape` and implement the `area()` function for each. In `main`, create a `std::vector<Shape*>` and store pointers to a `Circle` and a `Square` in it, then loop through the vector and print the area of each shape.
    2.  Create a class `MyArray` that wraps a dynamically allocated integer array. Overload the `[]` (subscript) operator to provide bounds-checked access to the array elements. It should throw an `std::out_of_range` exception if the index is invalid.
    3.  Implement the **Rule of Five** for a class `MyString` that manages its own C-style string (`char*`) on the heap. You must implement a: 1. Destructor, 2. Copy Constructor, 3. Copy Assignment Operator, 4. Move Constructor, and 5. Move Assignment Operator to handle deep copies and efficient moves.

-----

\<hr\>

### \#\# 2. Debugging Questions

  * **Easy (1 Question)**

    1.  The following code won't compile because it tries to access a private member. How would you fix this (e.g., by adding a public getter)?
        ```cpp
        class Person {
            std::string name;
        public:
            Person(std::string n) : name(n) {}
        };
        int main() {
            Person p("Alice");
            std::cout << p.name << std::endl; // Error!
            return 0;
        }
        ```

  * **Medium (5 Questions)**

    1.  This code is intended to set the `width` and `height`, but the constructor has a common bug. Find and fix it.
        ```cpp
        class Box {
            int width, height;
        public:
            // This constructor's body is incorrect
            Box(int width, int height) {
                width = width; // Bug: parameter assigns to itself
                height = height; // Bug: parameter assigns to itself
            }
        };
        ```
    2.  This code won't compile. The `printAge` function is declared `const`, but it's trying to do something that isn't allowed. What is the error and how do you fix it?
        ```cpp
        class User {
            int age;
        public:
            User(int a) : age(a) {}
            void printAge() const {
                age++; // Error!
                std::cout << age << std::endl;
            }
        };
        ```
    3.  When a `Student` object is created, the programmer expects the `name` to be "John". Instead, it's empty. Why? Fix the `Student` constructor.
        ```cpp
        class Person {
            std::string name;
        public:
            Person(std::string n) : name(n) {}
        };
        class Student : public Person {
            int studentID;
        public:
            // This constructor is not calling the base constructor
            Student(int id) : studentID(id) {}
        };
        ```
    4.  This code exhibits **object slicing**. The programmer expects to see "Dog says Woof\!", but sees "Animal makes a sound...". Why? Explain the bug.
        ```cpp
        class Animal {
        public:
            virtual void makeSound() { std::cout << "Animal makes a sound..." << std::endl; }
        };
        class Dog : public Animal {
        public:
            void makeSound() override { std::cout << "Dog says Woof!" << std::endl; }
        };
        int main() {
            Dog myDog;
            Animal myAnimal = myDog; // Bug: This is object slicing
            myAnimal.makeSound();
            return 0;
        }
        ```
    5.  This code won't compile. A `static` member function is trying to access a non-static member. Why is this an error and how could you fix it?
        ```cpp
        class Item {
            int itemID;
            static int nextID;
        public:
            static int getNextID() {
                itemID = 1; // Error!
                return nextID;
            }
        };
        ```

  * **Hard (3 Questions)**

    1.  The following code creates a `Derived` object but only the `Base` destructor is called, leading to a **memory leak**. Find the bug and fix it by adding one C++ keyword.
        ```cpp
        class Base {
        public:
            Base() {}
            ~Base() { std::cout << "Base destructor" << std::endl; } // Bug is here
        };
        class Derived : public Base {
            int* m_data;
        public:
            Derived() { m_data = new int[100]; }
            ~Derived() { delete[] m_data; std::cout << "Derived destructor" << std::endl; }
        };
        int main() {
            Base* b = new Derived();
            delete b; // Only calls ~Base()
            return 0;
        }
        ```
    2.  This code demonstrates the **diamond problem**. The call to `d.eat()` is ambiguous. How can you use `virtual` inheritance to fix this ambiguity?
        ```cpp
        class Animal { public: void eat() {} };
        class Mammal : public Animal {};
        class Reptile : public Animal {};
        // This inheritance is the source of the problem
        class Platypus : public Mammal, public Reptile {};

        int main() {
            Platypus d;
            d.eat(); // Error: 'eat' is ambiguous
            return 0;
        }
        ```
    3.  This class violates the **Rule of Three**. It works fine until an object is copied, at which point it will crash with a "double free" error. Find the bug and explain how to fix it by implementing a proper copy constructor.
        ```cpp
        class DataHolder {
            int* m_data;
        public:
            DataHolder(int val) { m_data = new int(val); }
            ~DataHolder() { delete m_data; }
            // Missing: Copy Constructor and Copy Assignment
        };
        int main() {
            DataHolder d1(10);
            DataHolder d2 = d1; // Bug: Shallow copy. d1.m_data == d2.m_data
        } // d2 is destroyed (deleting m_data), then d1 is destroyed (deleting m_data again)
        ```

-----

\<hr\>

### \#\# 3. Conceptual Questions

  * **Easy (1 Question)**

    1.  What is the difference between a **class** and an **object** in C++?

  * **Medium (5 Questions)**

    1.  Explain the principle of **Encapsulation**. How do the `public` and `private` access specifiers help achieve it?
    2.  Explain the principle of **Inheritance**. What is a base class and what is a derived class?
    3.  What is a **Constructor**? What is its main purpose, and how does it differ from a regular member function?
    4.  What is the **`this` pointer**? Inside which type of functions is it available?
    5.  What is the difference between `public`, `private`, and `protected` inheritance?

  * **Hard (3 Questions)**

    1.  Explain the difference between **static (compile-time) polymorphism** and **dynamic (run-time) polymorphism**. Give a C++ example for each.
    2.  What is an **abstract base class** and what is a **pure virtual function**? What is the main purpose of creating one?
    3.  What is the **Rule of Five** (or Rule of Three)? List the five special member functions, and explain why you would need to implement them.

-----

\<hr\>

### \#\# 4. Alternative Approach Questions

  * **Easy (1 Question)**

    1.  For a simple data structure that just holds a few public variables (like a coordinate `(x, y)`), you could use a `class` or a `struct`. What is the technical difference, and why might a `struct` be a more conventional choice in this case?

  * **Medium (5 Questions)**

    1.  Instead of making a member variable `private` and adding public `getter` and `setter` functions, you could just make the variable `public`. Why is the getter/setter approach almost always preferred for good class design?
    2.  You want a `Car` class to use an `Engine` class. You could use **inheritance** (`Car` "is-a" `Engine`) or **composition** (`Car` "has-a" `Engine`). Which relationship is correct here, and why is this "is-a" vs. "has-a" distinction so important in OOP?
    3.  To print the details of a `Book` object, you could write a member function `book.printDetails()`. Alternatively, you could write a free function `printDetails(const Book& book)`. What are the pros and cons of each approach?
    4.  To hide a helper function `do_calculation()` inside your class, you could make it `private`. An alternative is to place it in an anonymous (unnamed) namespace in your `.cpp` file. Compare these two ways of "hiding" a function.
    5.  To allow a free function `calculateTax(const Item& item)` to access `private` members of `Item`, you could make it a `friend` function. What is an alternative that avoids `friend`? (Hint: public getter functions).

  * **Hard (3Questions)**

    1.  To achieve polymorphism, you can use **virtual functions** (a dynamic, run-time approach). An alternative for a fixed set of types is to use `std::variant` and `std::visit` (a static, compile-time approach). Compare these two methods.
    2.  To create a generic "list" that can work with any type, you could use C-style `void*` pointers. The modern C++ alternative is **Templates** (`template <typename T> class List`). Explain why templates are a superior, type-safe alternative.
    3.  Instead of using virtual functions and inheritance to define an **interface** (e.g., `class IClickable`), you can use **static polymorphism** via the Curiously Recurring Template Pattern (CRTP). Briefly, what is the conceptual difference and a potential advantage of CRTP?

-----

\<hr\>

### \#\# 5. Other Question Types (Predict the Output / Best Practices)

  * **Easy (1 Question)**

    1.  **Predict the Output:** What will the following code print?
        ```cpp
        #include <iostream>
        class Counter {
        public:
            int val;
            Counter() { val = 5; }
        };
        int main() {
            Counter c;
            std::cout << c.val << std::endl;
            return 0;
        }
        ```

  * **Medium (5 Questions)**

    1.  **Predict the Output:** What will this code print? Pay attention to the order.
        ```cpp
        #include <iostream>
        class Base { public: Base() { std::cout << "Base Constructor" << std::endl; } };
        class Derived : public Base { public: Derived() { std::cout << "Derived Constructor" << std::endl; } };
        int main() { Derived d; return 0; }
        ```
    2.  **Predict the Output:** What will this code print? Pay attention to the order.
        ```cpp
        #include <iostream>
        class Base { public: ~Base() { std::cout << "Base Destructor" << std::endl; } };
        class Derived : public Base { public: ~Derived() { std::cout << "Derived Destructor" << std::endl; } };
        int main() { Derived d; return 0; }
        ```
    3.  **Best Practice:** Explain why you should prefer using **member initializer lists** in your constructor instead of assignment inside the constructor's body.
    4.  **Best Practice:** What is **"Object Slicing"** (as seen in the debugging section)? What is the correct way to pass a derived object polymorphically (e.g., to a function)?
    5.  **Predict the Output:** What is the output of this code, which uses a `static` member?
        ```cpp
        #include <iostream>
        class Thing {
        public:
            static int count;
            Thing() { count++; }
        };
        int Thing::count = 0; // Static member initialization
        int main() {
            Thing t1;
            Thing t2;
            std::cout << Thing::count << std::endl;
            return 0;
        }
        ```

  * **Hard (3 Questions)**

    1.  **Best Practice:** Explain the C++ Core Guideline "C.127: A class with a virtual function should have a virtual or protected destructor." Why is this critical for preventing resource leaks?
    2.  **Best Practice:** Explain the **Rule of Zero**. How does using modern C++ features (like smart pointers and standard containers) help you follow this rule and write safer classes?
    3.  **Predict the Output:** What will this code print? Explain *why* the `Derived::print()` is not called, even though `v_print()` is `virtual`.
        ```cpp
        #include <iostream>
        class Base {
        public:
            Base() { v_print(); } // Call in constructor
            virtual void v_print() { std::cout << "Base::v_print" << std::endl; }
        };
        class Derived : public Base {
        public:
            void v_print() override { std::cout << "Derived::v_print" << std::endl; }
        };
        int main() { Derived d; return 0; }
        ```