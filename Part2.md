## 🧠 **6. Polymorphism**

### **Definition (Many Forms)**

**Polymorphism** literally means _“many forms”_.
In OOP, it allows the same function, method, or operator to **behave differently based on the object or data type**.

👉 **In simple words:**

> One interface, many implementations.

---

### **Why is Polymorphism Important?**

- Enables **code reusability and flexibility**.
- Allows **dynamic behavior at runtime**.
- Makes programs **easier to maintain and extend**.
- Key to **achieving abstraction and modularity**.

---

## ⚙️ **Types of Polymorphism**

---

### **1️⃣ Compile-time (Static Polymorphism)**

Resolved **during compilation**.

#### ✅ **a) Function Overloading**

Multiple functions with the **same name** but **different parameters**.

```cpp
#include <iostream>
using namespace std;

class Math {
public:
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }

    int add(int a, int b, int c) {
        return a + b + c;
    }
};

int main() {
    Math m;
    cout << m.add(2, 3) << endl;         // 5
    cout << m.add(2.5, 3.5) << endl;     // 6.0
    cout << m.add(1, 2, 3) << endl;      // 6
}
```

💡 The compiler decides **which function** to call based on **argument types and count**.

---

#### ✅ **b) Operator Overloading**

Giving additional meaning to existing operators for **user-defined types**.

```cpp
#include <iostream>
using namespace std;

class Complex {
    int real, imag;
public:
    Complex(int r=0, int i=0) : real(r), imag(i) {}

    Complex operator + (const Complex &obj) {
        return Complex(real + obj.real, imag + obj.imag);
    }

    void show() { cout << real << " + " << imag << "i\n"; }
};

int main() {
    Complex c1(2,3), c2(1,2);
    Complex c3 = c1 + c2; // operator+ overloaded
    c3.show();  // 3 + 5i
}
```

---

### **2️⃣ Runtime (Dynamic Polymorphism)**

Resolved **during execution** (using virtual functions).

#### ✅ **a) Method Overriding**

A derived class provides a **specific implementation** of a function already defined in the base class.

```cpp
#include <iostream>
using namespace std;

class Animal {
public:
    virtual void speak() { cout << "Animal speaks\n"; }
};

class Dog : public Animal {
public:
    void speak() override { cout << "Dog barks\n"; }
};

int main() {
    Animal* a = new Dog();
    a->speak();  // Dog barks (runtime polymorphism)
}
```

👉 The `virtual` keyword ensures the **derived class version** is executed even when using a **base class pointer**.

---

## 🧩 **Virtual Functions and vtable Mechanism**

When a class has **virtual functions**, the compiler creates a hidden table called the **vtable** (Virtual Table).

Each object of that class has a hidden pointer (**vptr**) pointing to the vtable.

| Concept    | Description                                        |
| ---------- | -------------------------------------------------- |
| **vtable** | Table storing addresses of virtual functions       |
| **vptr**   | Pointer inside object that refers to the vtable    |
| **Use**    | Enables runtime resolution of overridden functions |

**Mechanism:**

1. When you call a virtual function via a base pointer,
   the compiler looks up the function’s address in the vtable.
2. The derived class’s overridden version replaces the base version in the vtable.

---

### **Example:**

```cpp
class Base {
public:
    virtual void show() { cout << "Base show\n"; }
};
class Derived : public Base {
public:
    void show() override { cout << "Derived show\n"; }
};
int main() {
    Base* ptr = new Derived();
    ptr->show();  // Derived show (resolved via vtable)
}
```

---

## 🔁 **Pure Virtual Functions**

A **pure virtual function** is a virtual function with **no definition** in the base class.
It forces derived classes to **implement** it.

**Syntax:**

```cpp
class Shape {
public:
    virtual void draw() = 0;  // pure virtual
};
class Circle : public Shape {
public:
    void draw() override { cout << "Drawing Circle\n"; }
};
int main() {
    Shape* s = new Circle();
    s->draw();
}
```

**Result:**

- The base class (`Shape`) becomes **abstract**.
- You **cannot create an object** of it.
- Must be **implemented in child classes**.

---

## 🔐 **final keyword (Java) / override keyword (C++)**

| Keyword              | Purpose                                                                                                          |
| -------------------- | ---------------------------------------------------------------------------------------------------------------- |
| **override (C++)**   | Ensures the derived method is overriding a virtual method of the base class. Helps catch errors at compile-time. |
| **final (C++/Java)** | Prevents further overriding or inheritance.                                                                      |

**Example (C++):**

```cpp
class Base {
public:
    virtual void show() final { cout << "Base final show\n"; }
};
class Derived : public Base {
    // void show() override; ❌ Error: cannot override final function
};
```

---

## 🧭 **Upcasting and Downcasting**

### **Upcasting**

Assigning a **derived class object** to a **base class pointer/reference**.
✅ Safe, commonly used for polymorphism.

```cpp
Animal* a = new Dog(); // Upcasting
a->speak();            // Dog barks
```

### **Downcasting**

Converting a **base pointer** back to a **derived pointer**.
⚠️ Risky – must ensure the object is actually of derived type.

```cpp
Animal* a = new Dog();
Dog* d = dynamic_cast<Dog*>(a);  // Safe downcasting using dynamic_cast
d->speak();  // Dog barks
```

If the cast is invalid, `dynamic_cast` returns `nullptr`.

---

## 🌍 **Real-world Example of Polymorphism**

Example: **Payment System**

```cpp
class Payment {
public:
    virtual void pay() { cout << "Generic Payment\n"; }
};
class CreditCard : public Payment {
public:
    void pay() override { cout << "Paying via Credit Card\n"; }
};
class PayPal : public Payment {
public:
    void pay() override { cout << "Paying via PayPal\n"; }
};
int main() {
    Payment* p;

    p = new CreditCard();
    p->pay();  // Paying via Credit Card

    p = new PayPal();
    p->pay();  // Paying via PayPal
}
```

👉 Same function `pay()` behaves differently depending on the **object type**.
That’s **polymorphism in action**.

---

## ✅ **Summary Table**

| Type         | Resolution         | Example                       | Keyword               |
| ------------ | ------------------ | ----------------------------- | --------------------- |
| Compile-time | At compile time    | Function/Operator Overloading | —                     |
| Runtime      | At execution time  | Virtual Function Overriding   | `virtual`, `override` |
| Pure Virtual | Must be overridden | Abstract classes              | `= 0`                 |
| Restriction  | Prevent overriding | Final methods                 | `final`               |

---

---

## 🧱 **7. Constructors and Destructors**

---

### 🧩 **What is a Constructor?**

A **constructor** is a **special member function** of a class that is **automatically called** when an object is created.
It’s mainly used to **initialize data members** of the object.

**Rules:**

- Name = same as class name.
- No return type (not even `void`).
- Can be overloaded.
- Can have parameters.

---

### **1️⃣ Default Constructor**

A constructor **with no parameters** (or one automatically provided by the compiler if none is defined).

```cpp
#include <iostream>
using namespace std;

class Student {
    int id;
public:
    Student() {          // Default Constructor
        id = 0;
        cout << "Default Constructor called\n";
    }

    void show() {
        cout << "Student ID: " << id << endl;
    }
};

int main() {
    Student s1;   // Automatically calls default constructor
    s1.show();
}
```

**Output:**

```
Default Constructor called
Student ID: 0
```

---

### **2️⃣ Parameterized Constructor**

A constructor that **takes parameters** to initialize the object with custom values.

```cpp
class Student {
    int id;
    string name;
public:
    Student(int i, string n) {   // Parameterized Constructor
        id = i;
        name = n;
        cout << "Parameterized Constructor called\n";
    }

    void show() {
        cout << id << " - " << name << endl;
    }
};

int main() {
    Student s1(1, "Bilal");
    Student s2(2, "Ahmad");
    s1.show();
    s2.show();
}
```

---

### **3️⃣ Copy Constructor**

Used to **create a new object as a copy of an existing object**.

**Syntax:**

```cpp
ClassName (const ClassName &oldObj);
```

**Example:**

```cpp
class Student {
    int id;
public:
    Student(int x) { id = x; }

    // Copy constructor
    Student(const Student &s) {
        id = s.id;
        cout << "Copy Constructor called\n";
    }

    void show() { cout << "ID: " << id << endl; }
};

int main() {
    Student s1(10);
    Student s2 = s1; // Copy constructor is called
    s2.show();
}
```

---

### **4️⃣ Constructor Overloading**

You can define **multiple constructors** in the same class with different parameter lists.

```cpp
class Rectangle {
    int length, width;
public:
    Rectangle() { length = width = 0; }
    Rectangle(int l) { length = width = l; }
    Rectangle(int l, int w) { length = l; width = w; }

    void area() { cout << "Area: " << length * width << endl; }
};

int main() {
    Rectangle r1, r2(5), r3(5,10);
    r1.area(); // 0
    r2.area(); // 25
    r3.area(); // 50
}
```

---

### **5️⃣ Destructor and its Importance**

A **destructor** is a **special member function** that is **automatically called when an object goes out of scope** or is **explicitly deleted**.
It is used to **free resources**, such as dynamic memory, files, or network handles.

**Rules:**

- Same name as class but **preceded by `~` (tilde)**.
- Takes **no arguments**.
- Cannot be overloaded.

**Example:**

```cpp
class Demo {
public:
    Demo() { cout << "Constructor called\n"; }
    ~Demo() { cout << "Destructor called\n"; }
};

int main() {
    Demo d; // Constructor called
}           // Destructor called automatically when program ends
```

---

### **6️⃣ Order of Constructor/Destructor Calls in Inheritance**

When inheritance is involved:

| **Phase**    | **Order**      |
| ------------ | -------------- |
| Constructors | Base → Derived |
| Destructors  | Derived → Base |

**Example:**

```cpp
class Base {
public:
    Base() { cout << "Base Constructor\n"; }
    ~Base() { cout << "Base Destructor\n"; }
};

class Derived : public Base {
public:
    Derived() { cout << "Derived Constructor\n"; }
    ~Derived() { cout << "Derived Destructor\n"; }
};

int main() {
    Derived d;
}
```

**Output:**

```
Base Constructor
Derived Constructor
Derived Destructor
Base Destructor
```

---

### **7️⃣ Shallow Copy vs Deep Copy**

#### **Shallow Copy**

- Copies all data **bit-by-bit** (default copy).
- Both objects share the **same memory** for pointer members.
- Can cause **double deletion** error if one object deletes memory.

```cpp
class Test {
    int* data;
public:
    Test(int val) {
        data = new int(val);
    }

    // Default copy constructor (shallow copy)
    void show() { cout << *data << endl; }

    ~Test() { delete data; }
};

int main() {
    Test t1(10);
    Test t2 = t1; // shallow copy

    // Both t1 and t2 point to the same memory → dangerous
}
```

#### **Deep Copy**

- Allocates **separate memory** and copies actual data, not pointer address.

```cpp
class Test {
    int* data;
public:
    Test(int val) {
        data = new int(val);
    }

    // Deep Copy Constructor
    Test(const Test &obj) {
        data = new int(*obj.data);
    }

    void show() { cout << *data << endl; }

    ~Test() { delete data; }
};
```

✅ **Deep copy** ensures each object has its **own copy of data**, preventing memory conflicts.

---

### ✅ **Quick Summary**

| Concept                       | Description                           |
| ----------------------------- | ------------------------------------- |
| **Default Constructor**       | Automatically called, no parameters   |
| **Parameterized Constructor** | Allows initialization with values     |
| **Copy Constructor**          | Copies data from another object       |
| **Overloaded Constructor**    | Multiple constructors for flexibility |
| **Destructor**                | Cleans up memory/resources            |
| **Constructor Order**         | Base → Derived                        |
| **Destructor Order**          | Derived → Base                        |
| **Shallow Copy**              | Copies addresses (unsafe)             |
| **Deep Copy**                 | Copies actual data (safe)             |

---

---

## ⚙️ **8. Static Members**

### **Definition**

The keyword **`static`** in OOP is used to define members (variables or functions) that **belong to the class rather than to any specific object**.

So, all objects of that class **share the same copy** of the static member.

---

### **1️⃣ Static Variables in a Class**

A **static data member** is a variable that is **shared among all objects** of a class.

- It’s **initialized only once**.
- Exists **independently of any object**.
- Stored in the **data segment (not heap or stack)**.
- Must be **defined outside the class**.

#### 🔹 **Example:**

```cpp
#include <iostream>
using namespace std;

class Student {
public:
    int id;
    static int count; // Declaration

    Student(int i) {
        id = i;
        count++;  // Increment static member
    }

    void show() {
        cout << "ID: " << id << " | Count: " << count << endl;
    }
};

// Definition outside the class
int Student::count = 0;

int main() {
    Student s1(101);
    Student s2(102);
    Student s3(103);

    s1.show();
    s2.show();
    s3.show();
}
```

**Output:**

```
ID: 101 | Count: 3
ID: 102 | Count: 3
ID: 103 | Count: 3
```

👉 **All objects share the same `count` variable.**
When one changes it, all others see the updated value.

---

### **2️⃣ Static Methods**

A **static function** in a class:

- Can be called **without creating an object**.
- Can **only access static data members** (not non-static).
- Does **not have `this` pointer** because it’s not tied to any object.

#### 🔹 **Example:**

```cpp
#include <iostream>
using namespace std;

class Demo {
    static int count;
public:
    static void showCount() {   // Static method
        cout << "Count: " << count << endl;
    }

    static void increment() {
        count++;
    }
};

int Demo::count = 0;  // Definition

int main() {
    Demo::showCount();   // Access without object
    Demo::increment();
    Demo::showCount();
}
```

**Output:**

```
Count: 0
Count: 1
```

---

### **3️⃣ Static Block (in Java)**

> ⚠️ Note: C++ **does not have static blocks** — this is specific to **Java**.

A **static block** in Java is used to **initialize static variables** when the class is first loaded (before any object creation).

**Example (Java syntax):**

```java
class Example {
    static int count;
    static {
        count = 10;
        System.out.println("Static block executed");
    }
}
```

Output when class is first used:

```
Static block executed
```

---

### **4️⃣ Difference Between Static and Non-static Members**

| Feature                            | **Static Member**          | **Non-static Member**    |
| ---------------------------------- | -------------------------- | ------------------------ |
| **Belongs to**                     | Class                      | Individual object        |
| **Memory**                         | One shared copy            | Separate copy per object |
| **Access**                         | Using class name or object | Only via object          |
| **Exists even without object?**    | ✅ Yes                     | ❌ No                    |
| **Has `this` pointer?**            | ❌ No                      | ✅ Yes                   |
| **Can access non-static members?** | ❌ No                      | ✅ Yes                   |

#### 🔹 **Example to Understand**

```cpp
class Test {
public:
    static int x;
    int y;

    void set(int a, int b) {
        x = a;  // Shared among all
        y = b;  // Specific to each object
    }

    void show() {
        cout << "x = " << x << ", y = " << y << endl;
    }
};

int Test::x = 0;

int main() {
    Test t1, t2;
    t1.set(5, 10);
    t2.set(20, 30);

    t1.show(); // x=20, y=10
    t2.show(); // x=20, y=30
}
```

✅ `x` is shared → both objects see the latest value.
✅ `y` is unique → each object has its own.

---

### **5️⃣ When to Use `static`**

Use `static` when:

1. You want a **common variable shared among all objects** (like a counter).
2. You need **utility/helper methods** that don’t depend on instance data.
3. You want to **limit memory usage** for frequently accessed constants.
4. You want a **global-like variable** but encapsulated within a class.

#### ✅ **Common Use Cases:**

- **Counting objects** created.
- **Configuration constants** (like PI, tax rate).
- **Singleton design pattern.**
- **Utility functions** (like Math operations).

---

### **6️⃣ Small Example Combining Static and Non-static**

```cpp
#include <iostream>
using namespace std;

class BankAccount {
    static int totalAccounts;
    int accountNumber;
public:
    BankAccount() {
        totalAccounts++;
        accountNumber = totalAccounts;
    }

    void show() {
        cout << "Account #: " << accountNumber
             << " | Total Accounts: " << totalAccounts << endl;
    }

    static void showTotal() {
        cout << "Total Accounts: " << totalAccounts << endl;
    }
};

int BankAccount::totalAccounts = 0;

int main() {
    BankAccount a1, a2, a3;
    a1.show();
    a2.show();
    BankAccount::showTotal();  // Access static function via class
}
```

---

### ✅ **Summary Table**

| Concept              | Description                              | Example                   |
| -------------------- | ---------------------------------------- | ------------------------- |
| Static Variable      | Shared across all objects                | `Student::count`          |
| Static Method        | Belongs to class, no object needed       | `Demo::showCount()`       |
| Static Block (Java)  | Executes once when class loads           | `static { ... }`          |
| Static vs Non-static | Static = shared, Non-static = per object | `x` vs `y` example        |
| When to Use          | Shared info or utility function          | Object counter, constants |

---

---

## ⚙️ **9. Operator Overloading (C++ Specific)**

### **1️⃣ What is Operator Overloading**

**Definition:**
Operator overloading means **redefining how an operator works for user-defined data types (like classes or structs)**.

👉 In simple words:
You can **make operators (+, -, \*, etc.) work with your own objects** just like they work with built-in types.

#### 🔹 **Example Without Overloading:**

```cpp
Complex c1(2, 3), c2(1, 4);
Complex c3 = c1 + c2;   // ❌ Error: '+' not defined for Complex
```

#### 🔹 **With Operator Overloading:**

You can define how `+` should behave for Complex numbers.

```cpp
Complex operator+(Complex obj) { ... }
```

Now `c1 + c2` works ✅.

---

### **2️⃣ Why We Use It**

- To make code **more readable and natural**.
- To perform operations **directly between objects**.
- To **extend C++ operators** to work with **user-defined data types**.

---

### **3️⃣ Syntax of Operator Overloading**

Operator overloading is done using a **special function** called an **operator function**.

#### **General Syntax:**

```cpp
return_type operator<symbol>(argument_list);
```

#### **Example (+ Operator):**

```cpp
class Complex {
    int real, imag;

public:
    Complex(int r = 0, int i = 0) {
        real = r;
        imag = i;
    }

    // Operator function
    Complex operator+(Complex obj) {
        Complex temp;
        temp.real = real + obj.real;
        temp.imag = imag + obj.imag;
        return temp;
    }

    void show() {
        cout << real << " + " << imag << "i" << endl;
    }
};

int main() {
    Complex c1(2, 3), c2(1, 4);
    Complex c3 = c1 + c2;  // c1.operator+(c2)
    c3.show();
}
```

**Output:**

```
3 + 7i
```

✅ Behind the scenes:
`c1 + c2` → `c1.operator+(c2)`

---

### **4️⃣ Which Operators Can / Cannot Be Overloaded**

#### ✅ **Operators That CAN Be Overloaded:**

| Category   | Examples                                      |                         |        |
| ---------- | --------------------------------------------- | ----------------------- | ------ |
| Arithmetic | `+`, `-`, `*`, `/`, `%`                       |                         |        |
| Relational | `==`, `!=`, `<`, `>`, `<=`, `>=`              |                         |        |
| Logical    | `&&`, `                                       |                         | `, `!` |
| Bitwise    | `&`, `                                        | `, `^`, `<<`, `>>`, `~` |        |
| Assignment | `=`, `+=`, `-=`, `*=`, `/=`, etc.             |                         |        |
| Unary      | `++`, `--`, `-` (negation), `*` (dereference) |                         |        |
| Other      | `[]`, `()`, `->`, `new`, `delete`             |                         |        |

---

#### ❌ **Operators That CANNOT Be Overloaded:**

| Operator                                                        | Reason                |
| --------------------------------------------------------------- | --------------------- |
| `::`                                                            | Scope resolution      |
| `.`                                                             | Member access         |
| `.*`                                                            | Member pointer access |
| `sizeof`                                                        | Compile-time operator |
| `?:`                                                            | Ternary conditional   |
| `typeid`                                                        | Type information      |
| `const_cast`, `static_cast`, `reinterpret_cast`, `dynamic_cast` | Type conversions      |

---

### **5️⃣ Friend Function Usage in Operator Overloading**

A **friend function** can also overload an operator.
Useful when **left operand is not an object of the same class**.

#### 🔹 **Example: Using Friend Function for `+`**

```cpp
#include <iostream>
using namespace std;

class Complex {
    int real, imag;
public:
    Complex(int r = 0, int i = 0) {
        real = r; imag = i;
    }

    // Friend function declaration
    friend Complex operator+(Complex c1, Complex c2);

    void show() {
        cout << real << " + " << imag << "i" << endl;
    }
};

// Friend function definition
Complex operator+(Complex c1, Complex c2) {
    Complex temp;
    temp.real = c1.real + c2.real;
    temp.imag = c1.imag + c2.imag;
    return temp;
}

int main() {
    Complex c1(3, 2), c2(1, 7);
    Complex c3 = c1 + c2;  // Calls friend function
    c3.show();
}
```

✅ **Output:**

```
4 + 9i
```

Here:

- Function is not a member of class.
- Declared as `friend` to access private data.
- Works when **both operands** are objects or even one is not (like `5 + c2`).

---

### **6️⃣ Unary Operator Overloading Example (++ / --)**

```cpp
#include <iostream>
using namespace std;

class Counter {
    int count;
public:
    Counter(int c = 0) { count = c; }

    // Overload ++ (prefix)
    Counter operator++() {
        ++count;
        return *this;
    }

    // Overload ++ (postfix)
    Counter operator++(int) {
        Counter temp = *this;
        count++;
        return temp;
    }

    void show() { cout << count << endl; }
};

int main() {
    Counter c1(5);
    ++c1;       // Prefix
    c1.show();  // 6

    c1++;       // Postfix
    c1.show();  // 7
}
```

---

### **7️⃣ Operator Overloading and Polymorphism**

Operator overloading is a form of **compile-time (static) polymorphism**,
because the operator function to call is determined **at compile time**.

---

### **8️⃣ Real-World Example: String Concatenation**

```cpp
#include <iostream>
#include <string>
using namespace std;

class MyString {
    string str;
public:
    MyString(string s = "") { str = s; }

    MyString operator+(MyString s) {
        return MyString(str + s.str);
    }

    void show() { cout << str << endl; }
};

int main() {
    MyString s1("Hello "), s2("World!");
    MyString s3 = s1 + s2; // Concatenation
    s3.show();
}
```

**Output:**

```
Hello World!
```

---

### ✅ **Summary Table**

| Concept              | Explanation                              | Example                         |
| -------------------- | ---------------------------------------- | ------------------------------- |
| Operator Overloading | Redefine operator for user-defined types | `Complex c3 = c1 + c2`          |
| Syntax               | `return_type operator<symbol>(params)`   | `Complex operator+(Complex)`    |
| Friend Function      | Allows external access to private data   | `friend Complex operator+(...)` |
| Unary Example        | ++, --                                   | `Counter c; ++c;`               |
| Cannot Overload      | `::`, `.`, `sizeof`, `?:`                | Not allowed                     |
| Type                 | Compile-time Polymorphism                | Decided at compile time         |

---

---

## 🧩 **10. Friend Function and Friend Class (C++ Specific)**

---

### **1️⃣ What is a Friend Function**

A **friend function** is a **non-member function** that has **permission to access private and protected members** of a class.

Normally, only member functions of a class can access its private data —
but a **friend function** can **bypass this restriction** if it is explicitly declared as a `friend` inside the class.

#### ✅ **Syntax:**

```cpp
class ClassName {
    friend returnType functionName(arguments);
};
```

The keyword **`friend`** is used inside the class **declaration only**, not during the function **definition**.

---

#### 🔹 **Example:**

```cpp
#include <iostream>
using namespace std;

class Box {
private:
    int width;
public:
    Box(int w) { width = w; }

    // Declaration of friend function
    friend void showWidth(Box b);
};

// Definition (not a member of Box)
void showWidth(Box b) {
    cout << "Width = " << b.width << endl; // accessing private member
}

int main() {
    Box b1(10);
    showWidth(b1);  // Friend function can access private data
}
```

**Output:**

```
Width = 10
```

✅ **Explanation:**

- `showWidth()` is **not** a member of `Box`.
- But it can still access `Box`’s **private data** because of the `friend` declaration.

---

### **2️⃣ Why Use Friend Function**

Friend functions are used when:

1. You want **non-member functions** to access private data.
2. You want **two different classes** to share some private data (e.g., comparison, arithmetic between objects).
3. You want to **overload operators** that require access to private data (like `+`, `==`, etc.).
4. When **encapsulation must be slightly relaxed** for flexibility.

---

#### 🔹 **Example: Comparison Between Two Classes**

```cpp
#include <iostream>
using namespace std;

class Square;
class Rectangle {
private:
    int width, height;
public:
    Rectangle(int w, int h): width(w), height(h) {}
    friend void compare(Rectangle, Square);
};

class Square {
private:
    int side;
public:
    Square(int s): side(s) {}
    friend void compare(Rectangle, Square);
};

void compare(Rectangle r, Square s) {
    if (r.width == s.side && r.height == s.side)
        cout << "Rectangle is a Square\n";
    else
        cout << "Rectangle is not a Square\n";
}

int main() {
    Rectangle r(4, 4);
    Square s(4);
    compare(r, s);
}
```

**Output:**

```
Rectangle is a Square
```

✅ Here, `compare()` is a **friend** of both classes, so it can access private members of both.

---

### **3️⃣ Accessing Private Members Using Friend**

Friend functions directly access private or protected data,
but **only those declared as friends** inside that class.

```cpp
class A {
private:
    int secret = 100;
public:
    friend void reveal(A obj);
};

void reveal(A obj) {
    cout << "Secret = " << obj.secret << endl;
}
```

**Key Point:**
Friendship is **not mutual**, **not inherited**, and **not transitive**.

- If class A is a friend of class B,
  it doesn’t mean class B is a friend of A.
- If class A is a friend of B, and B is a friend of C,
  A is **not** automatically a friend of C.

---

### **4️⃣ Difference Between Friend and Normal Function**

| Feature                    | Normal Function                  | Friend Function                                          |
| -------------------------- | -------------------------------- | -------------------------------------------------------- |
| **Membership**             | Not part of the class            | Not part of the class (but declared inside)              |
| **Access to Private Data** | ❌ Cannot access private members | ✅ Can access private & protected members                |
| **Declaration**            | Declared outside the class       | Declared inside class with `friend` keyword              |
| **Invocation**             | Called normally                  | Called normally (no `object.` needed)                    |
| **Encapsulation**          | Fully respected                  | Slightly breaks encapsulation (limited scope)            |
| **Common Use**             | Utility or helper functions      | Operator overloading, data comparison, or access sharing |

---

### **5️⃣ Friend Class**

A **friend class** allows **all member functions** of one class to access private and protected members of another class.

#### 🔹 **Example:**

```cpp
#include <iostream>
using namespace std;

class Engine {
private:
    int horsepower;
public:
    Engine(int hp): horsepower(hp) {}
    friend class Car;  // Car is a friend of Engine
};

class Car {
public:
    void showEnginePower(Engine e) {
        cout << "Engine horsepower = " << e.horsepower << endl;
    }
};

int main() {
    Engine e1(500);
    Car c1;
    c1.showEnginePower(e1);
}
```

**Output:**

```
Engine horsepower = 500
```

✅ Here, class `Car` can access private data of class `Engine` because it’s declared as a **friend class**.

---

### **6️⃣ Key Notes / Interview Points**

- Friendship is **granted**, not **taken**.
  (You must explicitly declare a friend inside the class.)
- Friendship is **not inherited**.
  Derived classes don’t automatically inherit friend status.
- Friendship is **one-way only**.
- Use friends **sparingly** — only when necessary, because it **weakens encapsulation**.

---

### ✅ **Quick Summary Table**

| Concept         | Description                                      | Example                  |
| --------------- | ------------------------------------------------ | ------------------------ |
| Friend Function | External function with access to private members | `friend void show(Box);` |
| Friend Class    | Gives another class full access to private data  | `friend class Car;`      |
| Declaration     | Inside class (with `friend`)                     | Inside class body        |
| Access          | Private, protected                               | Private, protected       |
| Use Cases       | Operator overloading, data sharing               | Close class cooperation  |
| Caution         | Breaks encapsulation                             | Use only when necessary  |

---

---
