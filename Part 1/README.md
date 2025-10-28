## 🧠 **1. OOP Basics (Object-Oriented Programming)**

### **What is OOP?**

**Object-Oriented Programming (OOP)** is a programming paradigm (style or approach) that organizes code into **objects** — each representing a real-world entity.
Each object contains:

- **Data (attributes / properties)** — what the object _has_
- **Methods (functions / behaviors)** — what the object _does_

💡 In simple terms:
OOP focuses on **objects** instead of **actions** and **data** instead of **logic**.

**Example:**
If you are building a car management app:

- Object → `Car`
- Attributes → `color`, `model`, `speed`
- Methods → `start()`, `stop()`, `accelerate()`

So, instead of writing functions like `startCar()` or `stopCar()` separately (procedural style), you wrap them inside the `Car` class.

---

### **Why OOP? (Advantages over Procedural Programming)**

| Feature                 | Procedural Programming                                    | Object-Oriented Programming                         |
| ----------------------- | --------------------------------------------------------- | --------------------------------------------------- |
| **Structure**           | Based on functions and procedures                         | Based on classes and objects                        |
| **Data Handling**       | Data is exposed and can be accessed by any function       | Data is hidden (Encapsulation)                      |
| **Reusability**         | Functions can be reused but data can’t be shared securely | Classes can be reused via inheritance               |
| **Maintainability**     | Hard to maintain large codebases                          | Easier to maintain and scale                        |
| **Extensibility**       | Difficult to add new features                             | Easy to extend through inheritance and polymorphism |
| **Real-World Modeling** | Not realistic                                             | Models real-world entities directly                 |

✅ **Main Advantages of OOP:**

1. **Modularity** – Each class handles one responsibility.
2. **Reusability** – Code can be reused through inheritance.
3. **Security** – Data hiding through encapsulation.
4. **Scalability** – Easier to expand the system.
5. **Maintainability** – Isolated components make debugging easy.

---

### **Real-Life Examples of OOP**

Let’s relate OOP to real life 👇

| Real-Life Example | Class         | Object            | Attributes                | Methods                    |
| ----------------- | ------------- | ----------------- | ------------------------- | -------------------------- |
| Car               | `Car`         | `myCar`, `bmwCar` | `color`, `model`, `speed` | `start()`, `stop()`        |
| Bank Account      | `BankAccount` | `acc1`, `acc2`    | `balance`, `accountNo`    | `deposit()`, `withdraw()`  |
| Student System    | `Student`     | `bilal`, `ahmad`  | `name`, `rollNo`, `grade` | `study()`, `attendClass()` |

💬 **Explanation:**
Each class acts like a blueprint, and each real-world entity (object) is created based on that blueprint.

---

### **Features of OOP (4 Pillars)**

These are the **core concepts** every interview covers:

1. **Encapsulation** → Binding data and methods into one unit (class).

   - Prevents external access to internal data.
   - Achieved using private/protected access modifiers.
   - Example: hiding a `password` variable inside a `User` class.

2. **Abstraction** → Hiding unnecessary implementation details and showing only the essential features.

   - Example: You press a “start” button on a car, but you don’t know how the engine starts internally.

3. **Inheritance** → Acquiring properties and behaviors from another class.

   - Example: `Car` → `ElectricCar` inherits from `Car`.

4. **Polymorphism** → One name, many forms.

   - Same function behaves differently depending on context.
   - Example: `draw()` method behaves differently for `Circle`, `Square`, and `Rectangle`.

---

### **Object, Class, and Instance**

#### **Class**

A **class** is a _blueprint_ or _template_ for creating objects.
It defines what data (attributes) and behavior (methods) an object will have.

Example:

```python
class Car:
    def __init__(self, color, model):
        self.color = color
        self.model = model

    def start(self):
        print(f"{self.model} is starting...")
```

Here, `Car` is a **class** that defines:

- Attributes → `color`, `model`
- Method → `start()`

---

#### **Object**

An **object** is an _instance_ of a class.
When you create an object, you allocate memory for the class and assign real values.

Example:

```python
car1 = Car("Red", "BMW X5")
car2 = Car("Blue", "Audi A4")
```

- `car1` and `car2` are **objects** of the `Car` class.
- Each has its own copy of data (`color`, `model`).

---

#### **Instance**

An **instance** is just another word for a specific object created from a class.
Every time you create an object from a class, you are creating an _instance_ of that class.

Example:

```python
car1 = Car("Red", "BMW X5")   # instance 1
car2 = Car("Blue", "Audi A4") # instance 2
```

Each instance has its own state and behavior.

---

### **Syntax of Class and Object Creation**

Let’s look at syntax in **3 common languages**:

#### 🐍 **Python**

```python
class Car:
    def __init__(self, color, model):
        self.color = color
        self.model = model

    def start(self):
        print(f"{self.model} started")

# Creating object
car1 = Car("Black", "Tesla")
car1.start()
```

#### ☕ **Java**

```java
class Car {
    String color;
    String model;

    void start() {
        System.out.println(model + " started");
    }
}

public class Main {
    public static void main(String[] args) {
        Car car1 = new Car(); // object creation
        car1.model = "Toyota";
        car1.start();
    }
}
```

#### 💻 **C++**

```cpp
#include <iostream>
using namespace std;

class Car {
public:
    string color;
    string model;

    void start() {
        cout << model << " started" << endl;
    }
};

int main() {
    Car car1; // object creation
    car1.model = "Honda";
    car1.start();
}
```

---

### ✅ **Summary**

| Concept           | Meaning                                   | Example                      |
| ----------------- | ----------------------------------------- | ---------------------------- |
| **OOP**           | A paradigm based on real-world entities   | Car, Student, Account        |
| **Class**         | Blueprint defining structure and behavior | `class Car { }`              |
| **Object**        | Instance of a class                       | `Car car1 = new Car();`      |
| **Encapsulation** | Data hiding                               | Private variables            |
| **Abstraction**   | Show essential info only                  | Abstract classes, interfaces |
| **Inheritance**   | Reuse existing code                       | `Child extends Parent`       |
| **Polymorphism**  | One name, many behaviors                  | Overloading & overriding     |

---

---

## 🧱 **2. Class and Object (Core Foundation)**

---

### **1. Class Definition and Declaration**

A **class** in C++ is a **user-defined data type** that groups related data (variables) and functions (methods) together.
It acts as a **blueprint** for creating **objects**.

#### 🔹 **Syntax:**

```cpp
class ClassName {
    // Access specifier
    // Data members (variables)
    // Member functions (methods)
};
```

#### 🔹 **Example:**

```cpp
#include <iostream>
using namespace std;

class Car {
public:                // Access specifier
    string brand;       // Data member
    int speed;          // Data member

    void start() {      // Member function
        cout << brand << " started at " << speed << " km/h" << endl;
    }
};
```

✅ Here:

- `Car` is the **class name**.
- `brand` and `speed` are **data members (attributes)**.
- `start()` is a **member function (method)**.
- The keyword `public` allows access to members from outside the class.

---

### **2. Creating Objects**

An **object** is an **instance of a class**.
Each object has its own **copy of data members**, but **shares the same methods**.

#### 🔹 **Syntax:**

```cpp
ClassName objectName;
```

#### 🔹 **Example:**

```cpp
int main() {
    Car car1;              // Object 1
    car1.brand = "Honda";
    car1.speed = 120;

    Car car2;              // Object 2
    car2.brand = "BMW";
    car2.speed = 200;

    car1.start();
    car2.start();

    return 0;
}
```

#### 🔹 **Output:**

```
Honda started at 120 km/h
BMW started at 200 km/h
```

✅ Each object (`car1`, `car2`) has:

- Its own copy of `brand` and `speed`
- Shared method `start()`

---

### **3. Accessing Data Members and Methods**

You use the **dot operator (`.`)** to access members of an object.

#### 🔹 **Syntax:**

```cpp
objectName.dataMember;
objectName.memberFunction();
```

#### 🔹 **Example:**

```cpp
Car car1;
car1.brand = "Toyota";
car1.speed = 150;
car1.start();
```

✅ **Explanation:**

- `car1.brand` → accesses data member `brand`
- `car1.start()` → calls member function `start()`

---

### **4. `this` Keyword (and Its Use Cases)**

The `this` keyword in C++ is a **pointer** that points to the **current object** — the object that is calling the method.

#### 🔹 **Important Points:**

- Every **non-static** member function has a hidden pointer called `this`.
- It’s automatically passed to all **non-static** functions of a class.
- It’s used to:

  1. **Differentiate between class variables and parameters with same name**
  2. **Return the current object**
  3. **Pass the current object to another function**

---

#### 🔹 **Example 1: Distinguish Between Variables**

```cpp
#include <iostream>
using namespace std;

class Student {
private:
    string name;
    int age;

public:
    void setData(string name, int age) {
        this->name = name;   // “this” points to current object
        this->age = age;
    }

    void showData() {
        cout << "Name: " << name << ", Age: " << age << endl;
    }
};

int main() {
    Student s1;
    s1.setData("Bilal", 23);
    s1.showData();
}
```

#### 🔹 **Output:**

```
Name: Bilal, Age: 23
```

✅ Here:

- Local variables `name` and `age` hide class members.
- Using `this->name` means _“name of the current object”_.

---

#### 🔹 **Example 2: Returning the Current Object**

```cpp
class Box {
private:
    int length;
public:
    Box setLength(int length) {
        this->length = length;
        return *this; // returns current object by reference
    }
    void show() {
        cout << "Length: " << length << endl;
    }
};

int main() {
    Box b;
    b.setLength(20).show(); // chaining using “this”
}
```

#### 🔹 **Output:**

```
Length: 20
```

✅ `return *this;` allows **method chaining**, which is common in fluent-style APIs.

---

### **5. Memory Allocation for Objects (Stack vs Heap)**

In C++, **objects can be created either:**

- **On Stack** → Automatically destroyed when out of scope
- **On Heap** → Created dynamically using `new`, manually destroyed using `delete`

---

#### 🧩 **A. Stack Allocation**

```cpp
Car c1;                // object on stack
c1.brand = "Audi";
c1.speed = 180;
c1.start();
```

✅ Characteristics:

- Memory allocated at **compile-time**.
- Automatically destroyed when it goes out of scope.
- Faster, but limited lifespan.

---

#### 🧩 **B. Heap Allocation (Dynamic Memory)**

```cpp
Car* c2 = new Car();   // object on heap (pointer to Car)
c2->brand = "Tesla";
c2->speed = 220;
c2->start();

delete c2; // must manually delete
```

✅ Characteristics:

- Memory allocated at **runtime** using `new`.
- You must manually free memory using `delete`.
- Useful for long-lived or dynamic objects.

---

#### ⚖️ **Stack vs Heap Summary**

| Feature          | Stack            | Heap                   |
| ---------------- | ---------------- | ---------------------- |
| **Allocation**   | Automatic        | Manual (`new`)         |
| **Deallocation** | Automatic        | Manual (`delete`)      |
| **Speed**        | Fast             | Slower                 |
| **Lifetime**     | Until scope ends | Until deleted          |
| **Syntax**       | `Car c1;`        | `Car* c1 = new Car();` |
| **Access**       | `c1.start();`    | `c1->start();`         |

---

### ✅ **Summary**

| Concept              | Explanation              | Example                         |
| -------------------- | ------------------------ | ------------------------------- |
| **Class**            | Blueprint for objects    | `class Car { ... };`            |
| **Object**           | Instance of class        | `Car car1;`                     |
| **Access Members**   | Using dot (`.`) operator | `car1.brand = "BMW";`           |
| **this keyword**     | Refers to current object | `this->name = name;`            |
| **Stack Allocation** | Auto destroyed object    | `Car c;`                        |
| **Heap Allocation**  | Dynamic object           | `Car* c = new Car(); delete c;` |

---

---

## 🧩 **3. Encapsulation**

---

### **1. Definition and Importance**

**Definition:**
**Encapsulation** means **wrapping data (variables)** and **code (functions)** that operate on that data into a single unit — called a **class** — and **restricting direct access** to some of the object’s components.

💡 In simple words:

> Encapsulation = Data + Methods bundled together + Controlled access.

It helps you **protect the internal state** of an object from being modified directly.

---

### **🔹 Example (Concept)**

```cpp
#include <iostream>
using namespace std;

class BankAccount {
private:
    int balance;  // hidden data

public:
    void deposit(int amount) {
        balance += amount;
    }

    void showBalance() {
        cout << "Balance: " << balance << endl;
    }
};

int main() {
    BankAccount acc;
    acc.deposit(500);
    acc.showBalance();
}
```

✅ Here:

- `balance` is **private** → cannot be accessed directly.
- Only **member functions** (`deposit`, `showBalance`) can modify it.
  That’s **Encapsulation**.

---

### **2. Access Modifiers → public, private, protected**

Access modifiers define **who can access** class members.

| Modifier      | Accessibility                                   | Usage                                                 |
| ------------- | ----------------------------------------------- | ----------------------------------------------------- |
| **public**    | Accessible from anywhere                        | For methods/data that need to be public               |
| **private**   | Accessible **only inside the class**            | For sensitive data that shouldn’t be changed directly |
| **protected** | Accessible inside class and **derived classes** | Used with inheritance                                 |

---

#### **Example:**

```cpp
#include <iostream>
using namespace std;

class Example {
public:
    int a;          // accessible anywhere
private:
    int b;          // accessible only inside class
protected:
    int c;          // accessible inside derived class

public:
    void setValues() {
        a = 1;
        b = 2;
        c = 3;
    }

    void showValues() {
        cout << a << " " << b << " " << c << endl;
    }
};

int main() {
    Example e;
    e.a = 10;      // ✅ allowed
    // e.b = 20;   // ❌ not allowed (private)
    // e.c = 30;   // ❌ not allowed (protected)
    e.showValues();
}
```

✅ **Key Rule:**

- `public` → Everyone can access.
- `private` → Only the same class can access.
- `protected` → Only the class and its children can access.

---

### **3. Getters and Setters (use + examples)**

Encapsulation doesn’t mean data is completely locked — it just means **data should be accessed safely** through **controlled methods** called **getters** and **setters**.

#### **Definition:**

- **Getter** → Used to _read_ private data.
- **Setter** → Used to _update_ private data.

---

#### **Example:**

```cpp
#include <iostream>
using namespace std;

class Employee {
private:
    int salary;   // private variable

public:
    // Setter
    void setSalary(int s) {
        if (s > 0)               // validation
            salary = s;
        else
            cout << "Invalid salary!" << endl;
    }

    // Getter
    int getSalary() {
        return salary;
    }
};

int main() {
    Employee e1;
    e1.setSalary(50000);
    cout << "Salary: " << e1.getSalary() << endl;

    e1.setSalary(-1000); // invalid update
}
```

#### **Output:**

```
Salary: 50000
Invalid salary!
```

✅ **Why Getters/Setters are used:**

- They **control** how data is modified.
- You can add **validation** or **business rules** inside setters.
- Prevents unwanted or invalid updates.

---

### **4. Data Hiding Concept**

**Data Hiding** is an important **goal of encapsulation**.

It means:

> Restricting access to the internal details of an object and exposing only necessary information.

By marking data members as **private**, you hide them from outside interference.

---

#### **Example (Bad Practice — No Encapsulation):**

```cpp
class Student {
public:
    int marks;
};

int main() {
    Student s;
    s.marks = -20; // ❌ anyone can assign invalid data
}
```

#### **Good Practice (Encapsulation + Data Hiding):**

```cpp
class Student {
private:
    int marks;

public:
    void setMarks(int m) {
        if (m >= 0 && m <= 100)
            marks = m;
        else
            cout << "Invalid marks!" << endl;
    }

    int getMarks() {
        return marks;
    }
};

int main() {
    Student s;
    s.setMarks(90);
    cout << "Marks: " << s.getMarks() << endl;
}
```

✅ Now, data is protected and can only be updated via **controlled methods**.

---

### **5. Why Encapsulation Improves Security**

Encapsulation protects an object’s data from:

- **Unauthorized access**
- **Invalid modifications**
- **Data corruption**

#### **Advantages:**

1. **Data protection:** Variables are hidden and can’t be accessed directly.
2. **Validation:** You can ensure correct data through setters.
3. **Modularity:** Each class manages its own data and behavior.
4. **Maintainability:** Internal implementation can change without affecting other parts.
5. **Security:** Only specific, tested methods can modify data.

---

#### **Example:**

```cpp
class Account {
private:
    int balance;

public:
    void deposit(int amount) {
        if (amount > 0)
            balance += amount;
        else
            cout << "Invalid deposit!" << endl;
    }

    int getBalance() {
        return balance;
    }
};

int main() {
    Account acc;
    acc.deposit(5000);  // ✅ allowed
    // acc.balance = -9999; // ❌ not allowed, secure!
    cout << "Balance: " << acc.getBalance() << endl;
}
```

✅ Even if someone tries to assign an invalid balance, they can’t.
That’s how **encapsulation secures internal data.**

---

### 🧠 **Quick Summary**

| Concept              | Description                               | Example                          |
| -------------------- | ----------------------------------------- | -------------------------------- |
| **Encapsulation**    | Wrapping data + methods in a single unit  | `class BankAccount { ... }`      |
| **Access Modifiers** | Control visibility of members             | `public`, `private`, `protected` |
| **Getters/Setters**  | Safe way to access or update private data | `setSalary()`, `getSalary()`     |
| **Data Hiding**      | Prevent direct access to sensitive data   | `private int balance;`           |
| **Security Benefit** | Prevent unauthorized access/modification  | Only methods can change values   |

---

---

## 🧠 **4. Abstraction**

---

### **1. Definition and Purpose**

**Definition:**
👉 **Abstraction** means **hiding unnecessary implementation details** from the user and showing only the **essential features** of an object.

💡 In simple words:

> You don’t need to know _how_ something works internally — only _what it does._

---

### **Purpose:**

- Reduce complexity by separating **“what to do”** from **“how to do it.”**
- Focus on the **interface (functionality)** instead of the **implementation**.
- Make code **easier to modify, reuse, and maintain.**

---

### **🔹 Real-World Example:**

- When you **drive a car**, you use the **steering**, **brake**, and **accelerator** —
  but you don’t know how the internal engine works.
  → You interact only with the **abstract interface** (pedals, wheel).

- A **TV remote** lets you change channels without knowing the internal circuit.

That’s **abstraction** — hiding complex logic and exposing only the necessary operations.

---

### **2. Difference Between Abstraction and Encapsulation**

| Aspect             | **Abstraction**                                                   | **Encapsulation**                                           |
| ------------------ | ----------------------------------------------------------------- | ----------------------------------------------------------- |
| **Meaning**        | Hides implementation details and shows only functionality         | Bundles data and methods into one unit                      |
| **Focus**          | _What to do_                                                      | _How to do it securely_                                     |
| **Implementation** | Achieved using abstract classes, interfaces                       | Achieved using access modifiers (private/public)            |
| **Purpose**        | To reduce complexity                                              | To protect data                                             |
| **Example**        | A “startEngine()” method — user doesn’t know engine’s inner logic | Keeping `engineTemperature` private and using getter/setter |

✅ **In short:**

- **Encapsulation** = hiding _data_
- **Abstraction** = hiding _implementation details_

---

### **3. Abstract Class (in C++)**

An **abstract class** is a **class that cannot be instantiated** (you can’t create objects of it).
It is designed to be a **base class** for other classes.

👉 Abstract classes usually contain at least **one pure virtual function.**

---

#### **Syntax:**

```cpp
class ClassName {
public:
    virtual void functionName() = 0; // pure virtual function
};
```

---

#### **Example:**

```cpp
#include <iostream>
using namespace std;

// Abstract class
class Shape {
public:
    // Pure virtual function
    virtual void draw() = 0;

    void info() {
        cout << "This is a shape.\n";
    }
};

// Derived class 1
class Circle : public Shape {
public:
    void draw() override {
        cout << "Drawing a Circle\n";
    }
};

// Derived class 2
class Rectangle : public Shape {
public:
    void draw() override {
        cout << "Drawing a Rectangle\n";
    }
};

int main() {
    // Shape s; // ❌ Error: cannot instantiate abstract class
    Shape* s1 = new Circle();
    Shape* s2 = new Rectangle();

    s1->draw();
    s2->draw();

    delete s1;
    delete s2;
}
```

#### **Output:**

```
Drawing a Circle
Drawing a Rectangle
```

✅ **Explanation:**

- `Shape` is an abstract class (it contains a pure virtual function `draw()`).
- We can’t create a `Shape` object directly.
- Subclasses **override** `draw()` to provide their own implementation.

---

### **4. Pure Virtual Function (in C++)**

A **pure virtual function** is a virtual function that has **no definition** in the base class.
It’s declared using `= 0`.

#### **Syntax:**

```cpp
virtual void functionName() = 0;
```

#### **Key Points:**

- Makes the class **abstract**.
- Must be **overridden** in the derived class.
- If derived class doesn’t override it → it also becomes abstract.

---

#### **Example:**

```cpp
class Animal {
public:
    virtual void sound() = 0; // pure virtual function
};

class Dog : public Animal {
public:
    void sound() override {
        cout << "Bark!" << endl;
    }
};

int main() {
    Animal* a = new Dog();
    a->sound();
    delete a;
}
```

#### **Output:**

```
Bark!
```

✅ **Explanation:**

- `Animal` defines what animals do (make a sound), not _how_ they do it.
- `Dog` provides its own version.
  This is **abstraction in action** — the user just calls `sound()` without caring about internal details.

---

### **5. Interface (in Java/Python)**

C++ doesn’t have a direct keyword `interface`,
but **interfaces** in Java/Python are equivalent to **classes with only pure virtual functions** in C++.

---

#### **In Java:**

```java
interface Shape {
    void draw(); // no implementation
}

class Circle implements Shape {
    public void draw() {
        System.out.println("Drawing Circle");
    }
}

class Main {
    public static void main(String[] args) {
        Shape s = new Circle();
        s.draw();
    }
}
```

✅ Interface = 100% abstract (only method declarations).

---

#### **In Python:**

Python doesn’t enforce interfaces directly, but you can simulate them using **abstract base classes (ABC)**.

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def draw(self):
        pass

class Circle(Shape):
    def draw(self):
        print("Drawing Circle")

s = Circle()
s.draw()
```

✅ Same concept — abstract base class defines a structure, subclasses define behavior.

---

### **6. Real-Life Examples**

#### 🏎️ **Car Example**

```cpp
class Car {
public:
    virtual void startEngine() = 0; // abstract behavior
    virtual void stopEngine() = 0;
};

class Tesla : public Car {
public:
    void startEngine() override {
        cout << "Starting Tesla with button press.\n";
    }
    void stopEngine() override {
        cout << "Stopping Tesla silently.\n";
    }
};

int main() {
    Car* c = new Tesla();
    c->startEngine();
    c->stopEngine();
    delete c;
}
```

Output:

```
Starting Tesla with button press.
Stopping Tesla silently.
```

✅ **Abstraction here:**

- User doesn’t know _how_ Tesla’s engine works (battery, motor, etc.).
- User only calls `startEngine()` and `stopEngine()` — the _what_, not _how_.

---

#### 🕹️ **Remote Control Example**

```cpp
class RemoteControl {
public:
    virtual void powerOn() = 0;
    virtual void powerOff() = 0;
};

class TVRemote : public RemoteControl {
public:
    void powerOn() override {
        cout << "TV is ON\n";
    }
    void powerOff() override {
        cout << "TV is OFF\n";
    }
};

int main() {
    RemoteControl* r = new TVRemote();
    r->powerOn();
    r->powerOff();
    delete r;
}
```

✅ User presses buttons without knowing how the signal travels — abstraction in real life.

---

### 🧠 **Summary Table**

| Concept                   | Description                                     | C++ Implementation                          |
| ------------------------- | ----------------------------------------------- | ------------------------------------------- |
| **Abstraction**           | Hiding complex details, showing only essentials | Abstract classes + pure virtual functions   |
| **Encapsulation**         | Data hiding through access control              | Private members + getters/setters           |
| **Abstract Class**        | Base class with pure virtual functions          | `class Shape { virtual void draw() = 0; };` |
| **Pure Virtual Function** | No implementation, must be overridden           | `virtual void draw() = 0;`                  |
| **Interface**             | 100% abstract class (in Java/Python)            | Class with only pure virtuals in C++        |
| **Purpose**               | Simplify usage, reduce complexity               | Hiding internal logic from user             |

---

---

## 🧩 **5. Inheritance**

### **Concept and Need**

**Definition:**
Inheritance is a mechanism in Object-Oriented Programming where one class (child/derived) can acquire properties and behaviors (data members and methods) of another class (parent/base).

It promotes **code reusability**, **extensibility**, and helps model **real-world relationships** (like a Car _is-a_ Vehicle).

**Syntax (C++):**

```cpp
class Parent {
public:
    void show() {
        cout << "This is Parent class\n";
    }
};

class Child : public Parent {   // Child inherits from Parent
public:
    void display() {
        cout << "This is Child class\n";
    }
};

int main() {
    Child c;
    c.show();      // Accessing Parent function
    c.display();   // Accessing Child function
}
```

---

### **Need for Inheritance**

- To **reuse existing code** instead of rewriting.
- To **extend functionality** of an existing class.
- To maintain a **hierarchical relationship** between classes.
- To achieve **polymorphism** (especially runtime).

---

## 🧱 **Types of Inheritance**

### **1️⃣ Single Inheritance**

One base class → One derived class.

```cpp
class A {
public:
    void show() { cout << "Class A\n"; }
};

class B : public A {
public:
    void display() { cout << "Class B\n"; }
};
```

---

### **2️⃣ Multiple Inheritance**

Derived class inherits from more than one base class.

```cpp
class A {
public:
    void showA() { cout << "Class A\n"; }
};
class B {
public:
    void showB() { cout << "Class B\n"; }
};
class C : public A, public B {
public:
    void showC() { cout << "Class C\n"; }
};
```

⚠️ **Problem:** If both A and B have a function with the same name, ambiguity occurs. (Explained later)

---

### **3️⃣ Multilevel Inheritance**

A derived class acts as a base class for another.

```cpp
class A {
public:
    void showA() { cout << "Class A\n"; }
};
class B : public A {
public:
    void showB() { cout << "Class B\n"; }
};
class C : public B {
public:
    void showC() { cout << "Class C\n"; }
};
```

---

### **4️⃣ Hierarchical Inheritance**

One base class → multiple derived classes.

```cpp
class Parent {
public:
    void show() { cout << "Parent class\n"; }
};
class Child1 : public Parent {};
class Child2 : public Parent {};
```

---

### **5️⃣ Hybrid Inheritance**

Combination of two or more types (e.g., multiple + multilevel).
⚠️ Leads to **Diamond Problem**, solved by **virtual inheritance**.

---

## ⚙️ **Constructor and Destructor Behavior in Inheritance**

- **Order of Constructor calls:** Base → Derived
- **Order of Destructor calls:** Derived → Base

```cpp
class A {
public:
    A() { cout << "A Constructor\n"; }
    ~A() { cout << "A Destructor\n"; }
};
class B : public A {
public:
    B() { cout << "B Constructor\n"; }
    ~B() { cout << "B Destructor\n"; }
};

int main() {
    B obj;
}
```

**Output:**

```
A Constructor
B Constructor
B Destructor
A Destructor
```

---

## 🧭 **super / base / derived class usage**

C++ uses **scope resolution (::)** instead of `super`.
You can explicitly call base class members:

```cpp
class Parent {
public:
    void display() { cout << "Parent display\n"; }
};

class Child : public Parent {
public:
    void display() {
        cout << "Child display\n";
        Parent::display();   // Calling base version
    }
};
```

---

## 🔁 **Method Overriding**

When a derived class defines a function with the **same name and parameters** as in the base class, the base version is **overridden**.

```cpp
class Base {
public:
    void show() { cout << "Base class\n"; }
};

class Derived : public Base {
public:
    void show() { cout << "Derived class\n"; }
};

int main() {
    Derived d;
    d.show();  // Derived class
}
```

**With Virtual Function (for Runtime Polymorphism):**

```cpp
class Base {
public:
    virtual void show() { cout << "Base\n"; }
};

class Derived : public Base {
public:
    void show() override { cout << "Derived\n"; }
};
```

---

## 🔗 **“Is-A” Relationship**

Inheritance represents an **“is-a”** relationship.
Example:

- A **Car is a Vehicle**
- A **Dog is an Animal**

```cpp
class Vehicle {
public:
    void start() { cout << "Vehicle starting\n"; }
};
class Car : public Vehicle {};
```

---

## ⚠️ **Problems in Multiple Inheritance (Ambiguity)**

If two base classes have functions with the same name, the compiler is confused which one to call.

```cpp
class A {
public:
    void show() { cout << "A\n"; }
};
class B {
public:
    void show() { cout << "B\n"; }
};
class C : public A, public B {};

int main() {
    C obj;
    // obj.show(); ❌ Ambiguous
    obj.A::show(); ✅ // Explicit resolution
}
```

---

## 🧩 **Virtual Inheritance (to solve Diamond Problem)**

**Diamond Problem Example:**

```cpp
class A { public: void show() { cout << "A\n"; } };
class B : virtual public A {};
class C : virtual public A {};
class D : public B, public C {};

int main() {
    D obj;
    obj.show(); // ✅ Only one copy of A is inherited
}
```

Without `virtual`, class D would inherit **two copies** of A (through B and C), causing ambiguity.

---

✅ **In short:**

| Concept             | Purpose                                       |
| ------------------- | --------------------------------------------- |
| Inheritance         | Reuse and extend existing code                |
| Constructor order   | Base → Derived                                |
| Destructor order    | Derived → Base                                |
| Overriding          | Redefine base behavior                        |
| Virtual inheritance | Avoid duplicate base copies                   |
| Is-A                | Logical relationship between base and derived |

---

---
