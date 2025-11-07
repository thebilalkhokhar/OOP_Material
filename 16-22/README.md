## **16. Composition vs Inheritance (HAS-A vs IS-A Relationship)**

### **1. Inheritance (IS-A Relationship)**

**Definition:**
Inheritance represents an **“IS-A” relationship** — where a derived (child) class **inherits** properties and behaviors from a base (parent) class.

**Example (C++):**

```cpp
class Animal {
public:
    void eat() { cout << "Eating..." << endl; }
};

class Dog : public Animal {
public:
    void bark() { cout << "Barking..." << endl; }
};

int main() {
    Dog d;
    d.eat();  // inherited
    d.bark();
}
```

✅ **Dog IS-A Animal** → true.
Dog inherits functionality directly.

**Use case:**
When two classes have a **clear hierarchical relationship** and **shared behavior**.

---

### **2. Composition (HAS-A Relationship)**

**Definition:**
Composition represents a **“HAS-A” relationship** — one class **contains an object** of another class, instead of inheriting from it.

**Example (C++):**

```cpp
class Engine {
public:
    void start() { cout << "Engine started!" << endl; }
};

class Car {
private:
    Engine engine;   // Car HAS-A Engine
public:
    void start() {
        engine.start();
        cout << "Car started!" << endl;
    }
};
```

✅ **Car HAS-A Engine** → true.
The Car class uses Engine’s behavior via composition.

---

### **3. Key Differences**

| Feature              | **Inheritance (IS-A)**                         | **Composition (HAS-A)**       |
| -------------------- | ---------------------------------------------- | ----------------------------- |
| **Relationship**     | “is a”                                         | “has a”                       |
| **Code Reuse**       | Achieved by extending classes                  | Achieved by including objects |
| **Coupling**         | Strong (tight) coupling                        | Loose coupling                |
| **Flexibility**      | Less flexible (changes in base affect derived) | More flexible                 |
| **Runtime Behavior** | Determined at compile-time                     | Can be changed at runtime     |
| **Example**          | Dog IS-A Animal                                | Car HAS-A Engine              |

---

### **4. When to Prefer Composition Over Inheritance**

✅ **Prefer composition when:**

1. The relationship is **not logically hierarchical**.
   → e.g., `Car` _has an_ `Engine`, but it’s **not** a type of engine.
2. You need **loose coupling** and **flexibility**.
   → Easier to replace or modify components without breaking the system.
3. To **avoid diamond/multiple inheritance issues** (ambiguity in C++).
4. For **code reuse without extending** the entire class hierarchy.

✅ **Rule of thumb:**

> “Favor **composition** over **inheritance**.”

---

### **5. Real-life Analogy**

- **Inheritance:**
  A “Student” **is a** “Person”.

- **Composition:**
  A “Car” **has an** “Engine”.

---

---

## **17. Aggregation and Association**

### **1. Association**

**Definition:**
Association is a **general relationship** between two classes — where one object **uses** or **interacts** with another.
There’s **no ownership** implied.

**Example (C++):**

```cpp
class Teacher {
public:
    string name;
    Teacher(string n): name(n) {}
};

class Student {
public:
    string name;
    Student(string n): name(n) {}
    void assignTeacher(Teacher &t) {
        cout << name << " is taught by " << t.name << endl;
    }
};

int main() {
    Teacher t("Mr. Ali");
    Student s("Bilal");
    s.assignTeacher(t);
}
```

✅ Relationship → _Student associated with Teacher_
(no ownership — both can exist independently)

---

### **2. Types of Association**

| Type             | Description                            | Example                 |
| ---------------- | -------------------------------------- | ----------------------- |
| **One-to-One**   | One object linked to exactly one other | Person ↔ Passport       |
| **One-to-Many**  | One object linked to many others       | Teacher → many Students |
| **Many-to-Many** | Many objects linked to many others     | Students ↔ Courses      |

---

### **3. Aggregation**

**Definition:**
Aggregation is a **special type of association** that represents a **“whole-part” relationship**.
The “whole” object **has** parts, but those parts **can exist independently**.

**Example (C++):**

```cpp
class Department {
public:
    string name;
    Department(string n): name(n) {}
};

class University {
public:
    string uniName;
    vector<Department*> departments;

    University(string name): uniName(name) {}

    void addDepartment(Department* d) {
        departments.push_back(d);
    }
};

int main() {
    Department cs("CS");
    Department ee("EE");

    University u("NUST");
    u.addDepartment(&cs);
    u.addDepartment(&ee);
}
```

✅ Relationship → _University has Departments_
If `University` is deleted, departments **still exist** independently.

---

### **4. Composition vs Aggregation**

| Feature             | **Aggregation**               | **Composition**            |
| ------------------- | ----------------------------- | -------------------------- |
| **Relationship**    | “Has-a” (weak ownership)      | “Has-a” (strong ownership) |
| **Object Lifetime** | Child can exist independently | Child dies with parent     |
| **Example**         | University → Department       | Car → Engine               |
| **Type**            | Weak association              | Strong association         |

---

### **5. Real-world Examples**

| Concept         | Example                    | Explanation                     |
| --------------- | -------------------------- | ------------------------------- |
| **Association** | Teacher teaches Student    | No ownership                    |
| **Aggregation** | University has Departments | Departments can exist elsewhere |
| **Composition** | Car has Engine             | Engine cannot exist without Car |

---

### **Summary Diagram (Conceptually)**

```
Association → general link
Aggregation → has-a (independent lifetime)
Composition → has-a (dependent lifetime)
```

---

---

## **18. Overloading vs Overriding (Must-Asked Topic)**

### **1. Definition**

| Concept         | Meaning                                                                                                      |
| --------------- | ------------------------------------------------------------------------------------------------------------ |
| **Overloading** | Same function name, different **parameter list** (within the same class). Happens at **compile-time**.       |
| **Overriding**  | Redefining a **base class function** in a **derived class** with the same signature. Happens at **runtime**. |

---

### **2. Function Overloading (Compile-Time Polymorphism)**

- Same function name
- Different **number/type/order** of parameters
- Return type alone **cannot** differentiate overloaded functions

**Example (C++):**

```cpp
#include <iostream>
using namespace std;

class Print {
public:
    void show(int x) {
        cout << "Integer: " << x << endl;
    }
    void show(string s) {
        cout << "String: " << s << endl;
    }
};

int main() {
    Print p;
    p.show(10);
    p.show("Hello");
}
```

✅ Output:

```
Integer: 10
String: Hello
```

👉 **Compiler decides** which function to call based on the arguments → **Compile-time binding**.

---

### **3. Function Overriding (Run-Time Polymorphism)**

- Same function name and same signature (parameters + return type)
- Defined in **base and derived** classes
- Base class function must be marked **`virtual`** (in C++)
- Uses **late binding (runtime resolution)**

**Example (C++):**

```cpp
#include <iostream>
using namespace std;

class Animal {
public:
    virtual void speak() { cout << "Animal speaks" << endl; }
};

class Dog : public Animal {
public:
    void speak() override { cout << "Dog barks" << endl; }
};

int main() {
    Animal *a = new Dog();
    a->speak(); // Output: Dog barks
    delete a;
}
```

✅ Because of `virtual`, the call is resolved **at runtime**, based on the **actual object type**.

---

### **4. Rules for Each**

| Feature                   | **Overloading**   | **Overriding**                      |
| ------------------------- | ----------------- | ----------------------------------- |
| **Where**                 | Same class        | Base–Derived classes                |
| **Parameters**            | Must be different | Must be same                        |
| **Return Type**           | Can differ        | Must be same                        |
| **Binding Time**          | Compile-time      | Run-time                            |
| **Keyword Used**          | None              | `virtual` (C++), `@Override` (Java) |
| **Inheritance Required?** | No                | Yes                                 |
| **Polymorphism Type**     | Static            | Dynamic                             |

---

### **5. Can Constructors Be Overloaded / Overridden?**

✅ **Constructor Overloading:**
Yes — allowed in C++ and Java.
Different parameter lists.

**Example:**

```cpp
class Student {
public:
    Student() { cout << "Default Constructor\n"; }
    Student(string name) { cout << "Parameterized Constructor\n"; }
};
```

❌ **Constructor Overriding:**
No — constructors **cannot be inherited**, hence **cannot be overridden**.

👉 However, **derived constructors can call base constructors** using `super` (Java) or initializer list (C++):

```cpp
class Base {
public:
    Base(int x) { cout << "Base Constructor\n"; }
};
class Derived : public Base {
public:
    Derived() : Base(5) { cout << "Derived Constructor\n"; }
};
```

---

### **6. Real-world Analogy**

- **Overloading:**
  Like multiple versions of a tool — same name, but different sizes (hammer for nails, sledgehammer for concrete).
- **Overriding:**
  Like replacing the default behavior — a child defines its own version of a rule inherited from the parent.

---

---

## **19. Access Specifiers (Detailed Explanation)**

Access specifiers define **visibility and accessibility** of class members (variables and methods).

---

### **1. In C++**

| Specifier     | Accessible Within Class | Accessible in Derived Class | Accessible Outside Class |
| ------------- | ----------------------- | --------------------------- | ------------------------ |
| **private**   | ✅                      | ❌                          | ❌                       |
| **protected** | ✅                      | ✅                          | ❌                       |
| **public**    | ✅                      | ✅                          | ✅                       |

**Example (C++):**

```cpp
#include <iostream>
using namespace std;

class Base {
private:
    int a = 1;
protected:
    int b = 2;
public:
    int c = 3;

    void show() {
        cout << a << " " << b << " " << c << endl;
    }
};

class Derived : public Base {
public:
    void display() {
        // cout << a; ❌ private not accessible
        cout << b << " " << c << endl; // ✅ protected, public accessible
    }
};
```

---

### **2. In Java**

| Specifier                     | Within Class | Same Package | Subclass (diff pkg)  | Outside Package |
| ----------------------------- | ------------ | ------------ | -------------------- | --------------- |
| **private**                   | ✅           | ❌           | ❌                   | ❌              |
| **default (package-private)** | ✅           | ✅           | ❌                   | ❌              |
| **protected**                 | ✅           | ✅           | ✅ (via inheritance) | ❌              |
| **public**                    | ✅           | ✅           | ✅                   | ✅              |

**Example (Java):**

```java
public class Person {
    private int id;
    int age;              // default
    protected String name;
    public String city;

    void show() {
        System.out.println("Private: " + id);
    }
}
```

---

### **3. Scope and Visibility Rules**

| Context       | Visibility                                          |
| ------------- | --------------------------------------------------- |
| **Private**   | Only inside same class                              |
| **Protected** | Class + subclasses (even in other packages in Java) |
| **Default**   | Only inside same package (Java only)                |
| **Public**    | Everywhere accessible                               |

---

### **4. Why Access Specifiers Matter**

✅ **Encapsulation:**
They enforce **data hiding** and protect internal object state.

✅ **Security:**
Limit external access to sensitive data.

✅ **Maintainability:**
Allow controlled access through **getters and setters**.

---

### **5. Real-world Analogy**

- **Private:** Your house key — only _you_ can use it.
- **Protected:** Your family can enter the house.
- **Public:** Anyone can visit the front lawn.
- **Default (Java):** Only people from your neighborhood (same package) can enter.

---

---

### 🧬 **20. Object Lifecycle & Garbage Collection**

#### **1. Object Creation and Destruction**

- **Creation:**

  - In **C++**, objects are created using constructors (default, parameterized, or copy constructors).

    ```cpp
    MyClass obj;          // Stack allocation
    MyClass* ptr = new MyClass();  // Heap allocation
    ```

  - In **Java/Python**, objects are created dynamically using the `new` keyword (Java) or simply by calling a class (Python).

    ```java
    MyClass obj = new MyClass();   // Java
    ```

    ```python
    obj = MyClass()  # Python
    ```

- **Destruction:**

  - In **C++**, destruction is manual:

    - Stack objects → automatically destroyed when they go out of scope.
    - Heap objects → destroyed using `delete` keyword.

    ```cpp
    delete ptr;  // Calls destructor
    ```

  - In **Java/Python**, there’s **no manual destruction** — the **Garbage Collector (GC)** automatically frees memory.

---

#### **2. Garbage Collector (Java / Python)**

- **Purpose:** Automatically detects and deletes unused (unreferenced) objects to free memory.

##### 🧠 How it works:

- It keeps track of all references to objects.
- When an object is **no longer reachable**, it’s marked for deletion.

##### **Java Garbage Collector**

- Runs in the background and frees objects that have no active references.
- Uses algorithms like **Mark and Sweep** and **Generational GC**.

##### **Python Garbage Collector**

- Uses **reference counting**:

  - Each object keeps track of how many references point to it.
  - When reference count = 0 → object is destroyed.

- Also has a **cycle detector** for circular references.

---

#### **3. `finalize()` Method in Java**

- It’s a **protected method** of class `Object`.
- Automatically called by the GC **before destroying an object**.
- Used to perform cleanup actions (like closing files or releasing resources).

Example:

```java
class MyClass {
    protected void finalize() {
        System.out.println("Object is being destroyed!");
    }
}
```

⚠️ **Note:**

- It’s **deprecated** in Java 9+ because it causes unpredictability.
- Use **try-with-resources** or **AutoCloseable** instead.

---

#### **4. Smart Pointers in C++**

- In modern C++ (C++11+), **smart pointers** automatically manage memory like a garbage collector.

##### Types:

1. **`std::unique_ptr`** – sole ownership (deleted when goes out of scope)

   ```cpp
   std::unique_ptr<MyClass> p1 = std::make_unique<MyClass>();
   ```

2. **`std::shared_ptr`** – shared ownership (deleted when last reference is destroyed)

   ```cpp
   std::shared_ptr<MyClass> p2 = std::make_shared<MyClass>();
   ```

3. **`std::weak_ptr`** – non-owning reference (prevents circular reference)

   ```cpp
   std::weak_ptr<MyClass> wp = p2;
   ```

---

### ⚖️ **Summary Table**

| Concept                 | C++                                    | Java                      | Python         |
| ----------------------- | -------------------------------------- | ------------------------- | -------------- |
| Object Creation         | Manual / automatic                     | `new` keyword             | Class call     |
| Destruction             | Manual (`delete`) or automatic (stack) | Automatic (GC)            | Automatic (GC) |
| Garbage Collection      | Not automatic (use smart pointers)     | Automatic                 | Automatic      |
| finalize() / destructor | Destructor `~Class()`                  | `finalize()` (deprecated) | `__del__()`    |
| Smart Pointers          | ✅ Yes (C++11+)                        | ❌                        | ❌             |

---

---

## 🧠 **21. Design Principles & Patterns**

---

### 🧩 **A. SOLID Principles**

SOLID is a set of **five design principles** that help make software **maintainable, scalable, and flexible**.

---

#### **1️⃣ Single Responsibility Principle (SRP)**

- A class should have **only one reason to change**.
- Means: each class should do **only one job**.

✅ **Example (Violation):**

```cpp
class Report {
    void generateReport() {}
    void saveToFile() {}   // saving is not this class's responsibility
}
```

✅ **Corrected:**

```cpp
class ReportGenerator { void generateReport() {} };
class FileSaver { void saveToFile() {} };
```

---

#### **2️⃣ Open/Closed Principle (OCP)**

- Classes should be **open for extension**, but **closed for modification**.
- Add new functionality by **extending** (inheritance or composition), not by modifying old code.

✅ Example (Good):

```cpp
class Shape {
    virtual void draw() = 0;
};
class Circle : public Shape {
    void draw() override { cout << "Circle\n"; }
};
class Square : public Shape {
    void draw() override { cout << "Square\n"; }
};
```

You can add new shapes without changing the old code.

---

#### **3️⃣ Liskov Substitution Principle (LSP)**

- Subclasses should be **substitutable** for their base classes without changing program behavior.

❌ **Violation Example:**

```cpp
class Bird {
    virtual void fly() {}
};
class Ostrich : public Bird {
    void fly() override { throw "Ostrich can't fly!"; }
}
```

✅ Better:

```cpp
class Bird {};
class FlyingBird : public Bird { virtual void fly() = 0; };
```

---

#### **4️⃣ Interface Segregation Principle (ISP)**

- Don’t force a class to implement methods it doesn’t use.
- Prefer **smaller, specific interfaces** over large general ones.

✅ Example:

```cpp
class Printer { virtual void print() = 0; };
class Scanner { virtual void scan() = 0; };
class MultiFunctionPrinter : public Printer, public Scanner {};
```

---

#### **5️⃣ Dependency Inversion Principle (DIP)**

- High-level modules should **not depend** on low-level modules — both should depend on **abstractions**.
- Use interfaces or abstract classes to reduce coupling.

✅ Example:

```cpp
class Database { virtual void save() = 0; };
class MySQLDatabase : public Database { void save() override {} };

class App {
    Database* db;
public:
    App(Database* d) : db(d) {}
    void saveData() { db->save(); }
};
```

---

### 💡 **B. Other Design Rules**

#### **1. DRY — Don’t Repeat Yourself**

- Avoid duplicating code; reuse through functions, inheritance, or modules.

#### **2. KISS — Keep It Simple, Stupid**

- Prefer **simple, readable, and maintainable** solutions over clever but complex ones.

#### **3. YAGNI — You Aren’t Gonna Need It**

- Don’t build features “just in case.” Add them **only when needed**.

---

### 🧱 **C. Basic Design Patterns**

---

#### **1️⃣ Singleton Pattern**

- Ensures only **one instance** of a class exists in the whole program.

✅ Example:

```cpp
class Singleton {
    static Singleton* instance;
    Singleton() {}
public:
    static Singleton* getInstance() {
        if (!instance) instance = new Singleton();
        return instance;
    }
};
Singleton* Singleton::instance = nullptr;
```

---

#### **2️⃣ Factory Pattern**

- Creates objects **without exposing the creation logic**.
- Good for decoupling object creation from usage.

✅ Example:

```cpp
class Shape { virtual void draw() = 0; };
class Circle : public Shape { void draw() override { cout << "Circle"; } };
class Square : public Shape { void draw() override { cout << "Square"; } };

class ShapeFactory {
public:
    static Shape* getShape(string type) {
        if (type == "circle") return new Circle();
        if (type == "square") return new Square();
        return nullptr;
    }
};
```

---

#### **3️⃣ Builder Pattern**

- Used to **construct complex objects step by step**.

✅ Example:

```cpp
class Burger {
public:
    string bread, meat;
};
class BurgerBuilder {
    Burger b;
public:
    BurgerBuilder& addBread(string bread) { b.bread = bread; return *this; }
    BurgerBuilder& addMeat(string meat) { b.meat = meat; return *this; }
    Burger build() { return b; }
};
```

---

#### **4️⃣ Prototype Pattern**

- Creates a new object by **cloning an existing one**.

✅ Example:

```cpp
class Shape {
public:
    virtual Shape* clone() = 0;
};
class Circle : public Shape {
    Shape* clone() override { return new Circle(*this); }
};
```

---

#### **5️⃣ Adapter Pattern**

- Converts the interface of a class into another interface the client expects.
- Used when two classes **can’t work together due to interface mismatch**.

✅ Example:

```cpp
class OldPrinter {
public:
    void oldPrint() { cout << "Old printer\n"; }
};
class NewPrinter {
public:
    virtual void print() = 0;
};
class PrinterAdapter : public NewPrinter {
    OldPrinter* oldPrinter;
public:
    PrinterAdapter(OldPrinter* p) : oldPrinter(p) {}
    void print() override { oldPrinter->oldPrint(); }
};
```

---

#### **6️⃣ Observer Pattern**

- Defines a **one-to-many** relationship.
- When one object changes, all its dependents are **notified automatically**.

✅ Example:

```cpp
class Observer { public: virtual void update() = 0; };
class Subject {
    vector<Observer*> observers;
public:
    void addObserver(Observer* o) { observers.push_back(o); }
    void notify() { for (auto o : observers) o->update(); }
};
```

---

#### **7️⃣ Strategy Pattern**

- Defines a **family of algorithms** and lets you choose one at runtime.

✅ Example:

```cpp
class Strategy {
public:
    virtual void execute() = 0;
};
class FastAlgorithm : public Strategy {
    void execute() override { cout << "Fast!\n"; }
};
class SlowAlgorithm : public Strategy {
    void execute() override { cout << "Slow!\n"; }
};

class Context {
    Strategy* strategy;
public:
    Context(Strategy* s) : strategy(s) {}
    void run() { strategy->execute(); }
};
```

---

### ⚖️ **Summary Table**

| Principle/Pattern | Purpose                        |
| ----------------- | ------------------------------ |
| **SRP**           | Each class has one job         |
| **OCP**           | Extend without modifying       |
| **LSP**           | Derived class can replace base |
| **ISP**           | Use small, focused interfaces  |
| **DIP**           | Depend on abstractions         |
| **DRY**           | Avoid duplicate code           |
| **KISS**          | Keep design simple             |
| **YAGNI**         | Don’t over-engineer            |
| **Singleton**     | Only one instance              |
| **Factory**       | Centralized object creation    |
| **Builder**       | Stepwise object creation       |
| **Prototype**     | Clone existing objects         |
| **Adapter**       | Bridge incompatible interfaces |
| **Observer**      | Notify dependents on change    |
| **Strategy**      | Switch behavior dynamically    |

---

---

## 🧩 **22. Common OOP Interview Questions**

---

### ✅ **1. Difference between Abstraction and Encapsulation**

| Feature         | **Abstraction**                                               | **Encapsulation**                                      |
| --------------- | ------------------------------------------------------------- | ------------------------------------------------------ |
| **Meaning**     | Hides _implementation details_ and shows _essential features_ | Binds _data and methods_ together inside a class       |
| **Focus**       | Focuses on _what an object does_                              | Focuses on _how it hides its data_                     |
| **Achieved by** | Abstract classes, Interfaces                                  | Access modifiers (private, public, protected)          |
| **Example**     | A “Car” class exposes `drive()`, hides the engine logic       | Data members are private; accessed via getters/setters |

🧠 _Think:_

> Abstraction = Hiding **implementation**
> Encapsulation = Hiding **data**

---

### ✅ **2. Can Constructor be Virtual?**

❌ **No**, constructors cannot be virtual in C++.

**Reason:**
Virtual functions work via the **vtable**, which is set up **after** the constructor finishes.
So, during object creation, the **object type is not fully known**, hence virtual dispatch isn’t possible.

🧠 _However_, destructors **can** and **should** be virtual when using inheritance (see next).

---

### ✅ **3. Why We Use Virtual Destructors?**

If a base class pointer points to a derived class object and you delete it —
Without a virtual destructor, **only the base part is destroyed**, not the derived one.

✅ **Example:**

```cpp
class Base {
public:
    virtual ~Base() { cout << "Base destroyed\n"; }
};
class Derived : public Base {
public:
    ~Derived() { cout << "Derived destroyed\n"; }
};
```

Without `virtual`, only `"Base destroyed"` prints → **memory leak**.

---

### ✅ **4. What is Object Slicing?**

When a **derived class object** is assigned to a **base class object**,
the **derived part gets sliced off** — only base members remain.

❌ Example:

```cpp
class Base { int x; };
class Derived : public Base { int y; };

Derived d;
Base b = d;  // y is sliced off
```

🧠 **Prevent it** by using pointers or references instead of objects.

---

### ✅ **5. Difference between Compile-time and Runtime Polymorphism**

| Type             | **Compile-time (Static)**                         | **Runtime (Dynamic)**                 |
| ---------------- | ------------------------------------------------- | ------------------------------------- |
| **Binding time** | During compilation                                | During execution                      |
| **Achieved by**  | Function / Operator Overloading                   | Virtual functions / Overriding        |
| **Performance**  | Faster (no runtime lookup)                        | Slower (due to vtable)                |
| **Example**      | `int add(int, int)` and `float add(float, float)` | `Base* b = new Derived(); b->show();` |

---

### ✅ **6. Diamond Problem in Multiple Inheritance**

Occurs when a class inherits from **two classes** that both inherit from the **same base**.

```cpp
class A { };
class B : public A { };
class C : public A { };
class D : public B, public C { }; // ❌ A appears twice
```

🧠 **Solution:** Use **Virtual Inheritance**

```cpp
class B : virtual public A { };
class C : virtual public A { };
```

Now `D` gets only one copy of `A`.

---

### ✅ **7. What Happens if You Don’t Define a Destructor?**

If you don’t define one, the **compiler provides a default destructor**.
But if your class allocates dynamic memory (using `new`, file handles, etc.),
the default destructor won’t free it → **memory leak**.

🧠 Always define a **custom destructor** for classes managing resources (Rule of 3/5 in C++).

---

### ✅ **8. Interface vs Abstract Class**

| Feature         | **Abstract Class**                   | **Interface**                          |
| --------------- | ------------------------------------ | -------------------------------------- |
| **Methods**     | Can have abstract + concrete methods | All methods abstract (till Java 8)     |
| **Variables**   | Can have instance variables          | Only constants (final static)          |
| **Inheritance** | Single inheritance                   | Multiple interfaces can be implemented |
| **Use when**    | Classes share common behavior        | Classes share only capability          |

🧠 Example (Java):

```java
abstract class Animal { void eat() {} abstract void sound(); }
interface Flyable { void fly(); }
```

---

### ✅ **9. How to Achieve Multiple Inheritance in Java**

Java **does not support** multiple inheritance with **classes**,
but you can achieve it using **interfaces**.

✅ Example:

```java
interface A { void show(); }
interface B { void display(); }
class C implements A, B {
    public void show() {}
    public void display() {}
}
```

---

### ✅ **10. Can We Override Static Methods?**

❌ **No**, static methods **cannot be overridden**,
because they belong to the **class**, not the **object**.

However, they can be **redeclared** (known as _method hiding_).

✅ Example:

```java
class A { static void show() { System.out.println("A"); } }
class B extends A { static void show() { System.out.println("B"); } }

A a = new B();
a.show(); // Prints "A" → static binding
```

---

### ✅ **11. Why Prefer Composition over Inheritance?**

🧩 **Inheritance** = “Is-A”
🧱 **Composition** = “Has-A”

**Why prefer composition:**

1. Avoids tight coupling between parent and child.
2. More flexible — can change components at runtime.
3. Prevents fragile base class problems.
4. Encourages code reuse without exposing internal structure.

✅ Example:

```cpp
class Engine { void start() {} };
class Car {
    Engine e;  // composition
public:
    void start() { e.start(); }
};
```

---

### ⚡ **Summary Table**

| Question                     | Key Idea                                |
| ---------------------------- | --------------------------------------- |
| Abstraction vs Encapsulation | Implementation hiding vs Data hiding    |
| Virtual Constructor          | ❌ Not allowed                          |
| Virtual Destructor           | ✅ To avoid memory leaks                |
| Object Slicing               | Derived info lost when assigned to base |
| Compile-time vs Runtime      | Overloading vs Overriding               |
| Diamond Problem              | Ambiguity solved by Virtual Inheritance |
| Missing Destructor           | Default one may cause leaks             |
| Interface vs Abstract        | Full vs partial abstraction             |
| Multiple Inheritance (Java)  | Achieved using interfaces               |
| Override Static              | ❌ Only hidden, not overridden          |
| Composition > Inheritance    | For flexibility & low coupling          |

---
