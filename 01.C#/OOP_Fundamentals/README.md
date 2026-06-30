# OOP Fundamentals – C# Interview Preparation Guide

**56 Questions & Answers | From Basics to Senior MNC Level**

Topics covered: Encapsulation · Inheritance · Polymorphism · Abstraction · Interfaces · Constructors · SOLID Principles · Dependency Injection · Memory Management · Composition vs Inheritance

---

## 📑 Table of Contents

1. [OOP Fundamentals](#oop-fundamentals) (Q1–Q4)
2. [Encapsulation](#encapsulation) (Q5–Q7)
3. [Inheritance](#inheritance) (Q8–Q11)
4. [Polymorphism](#polymorphism) (Q12–Q18)
5. [Abstraction](#abstraction) (Q19–Q22)
6. [Interfaces](#interfaces) (Q23–Q26)
7. [Constructors](#constructors) (Q27–Q30)
8. [Keywords](#keywords) (Q31–Q34)
9. [Access Modifiers](#access-modifiers) (Q35–Q36)
10. [Memory Management](#memory-management) (Q37–Q40)
11. [Composition vs Inheritance](#composition-vs-inheritance) (Q41–Q43)
12. [Dependency Injection](#dependency-injection) (Q44–Q45)
13. [SOLID Principles](#solid-principles) (Q46–Q51)
14. [Senior-Level MNC Questions](#senior-level-mnc-questions) (Q52–Q56)

---

## OOP Fundamentals

### Q1. What is Object-Oriented Programming (OOP)?

Object-Oriented Programming is a programming paradigm that organizes software around objects rather than functions and logic.

**The four core pillars are:**
- Encapsulation
- Inheritance
- Polymorphism
- Abstraction

**Benefits:**
- Reusability
- Maintainability
- Scalability
- Security
- Testability

### Q2. What is a Class?

A class is a blueprint or template that defines the properties and behaviors of an object.

```csharp
public class Employee
{
    public string Name { get; set; }
    public void Work() { }
}
```

### Q3. What is an Object?

An object is an instance of a class that occupies memory and contains actual data.

```csharp
Employee emp = new Employee();
// emp is an object of Employee
```

### Q4. What is the difference between a Class and an Object?

| Class | Object |
|---|---|
| Blueprint | Instance |
| Logical entity | Physical entity |
| No memory allocated | Memory allocated |
| Defines structure | Holds actual data |

---

## Encapsulation

### Q5. What is Encapsulation?

Encapsulation is the process of hiding internal data and exposing controlled access through methods or properties.

```csharp
public class BankAccount
{
    private decimal balance;

    public decimal Balance
    {
        get { return balance; }
        private set { balance = value; }
    }
}
```

### Q6. Why is Encapsulation important?

- Protects data from unauthorized access
- Reduces coupling
- Improves maintainability
- Enforces business rules

### Q7. How is Encapsulation achieved in C#?

Using:
- Access modifiers
- Properties
- Private fields
- Methods

```csharp
private string password;
```

---

## Inheritance

### Q8. What is Inheritance?

Inheritance allows a derived class to acquire properties and methods of a base class.

```csharp
public class Animal
{
    public void Eat() { }
}

public class Dog : Animal
{
}
```

### Q9. What are the advantages of Inheritance?

- Code reuse
- Reduced duplication
- Easier maintenance
- Extensibility

### Q10. What types of Inheritance are supported in C#?

**Supported:**
- Single Inheritance
- Multilevel Inheritance
- Hierarchical Inheritance

**Not Supported for Classes:**
- Multiple Inheritance (achieved using interfaces)

### Q11. Why doesn't C# support multiple inheritance for classes?

To avoid ambiguity problems such as the Diamond Problem. Instead, C# supports multiple interface inheritance.

---

## Polymorphism

### Q12. What is Polymorphism?

Polymorphism means "many forms." It allows the same method or interface to behave differently depending on the object.

### Q13. What are the types of Polymorphism in C#?

| Type | Mechanism |
|---|---|
| Compile-Time Polymorphism | Method Overloading |
| Run-Time Polymorphism | Method Overriding |

### Q14. What is Method Overloading?

Multiple methods with the same name but different parameter lists.

```csharp
public void Print(string name) { }
public void Print(int id) { }
```

### Q15. What is Method Overriding?

Providing a new implementation for a virtual method in a derived class.

```csharp
public class Animal
{
    public virtual void Speak()
    {
        Console.WriteLine("Animal Sound");
    }
}

public class Dog : Animal
{
    public override void Speak()
    {
        Console.WriteLine("Bark");
    }
}
```

### Q16. Difference between Overloading and Overriding?

| Overloading | Overriding |
|---|---|
| Compile-time | Run-time |
| Same class | Parent-child relationship |
| Different parameters | Same signature |
| No inheritance required | Inheritance required |

### Q17. What is a Virtual Method?

A method marked with the `virtual` keyword that can be overridden by derived classes.

```csharp
public virtual void Calculate() { }
```

### Q18. What is the Override Keyword?

The `override` keyword provides a new implementation for a virtual or abstract method.

---

## Abstraction

### Q19. What is Abstraction?

Abstraction hides implementation details and exposes only essential functionality.

> Example: A user drives a car without knowing how the engine works.

### Q20. How is Abstraction achieved in C#?

- Abstract Classes
- Interfaces

### Q21. What is an Abstract Class?

An abstract class cannot be instantiated and may contain both abstract and concrete methods.

```csharp
public abstract class Employee
{
    public abstract void CalculateSalary();
}
```

### Q22. What is an Abstract Method?

A method without implementation that must be implemented by derived classes.

```csharp
public abstract void ProcessPayment();
```

---

## Interfaces

### Q23. What is an Interface?

An interface defines a contract that implementing classes must follow.

```csharp
public interface ILogger
{
    void Log(string message);
}
```

### Q24. Why do we use Interfaces?

- Loose coupling
- Better testability
- Dependency Injection
- Multiple inheritance support

### Q25. Difference between Interface and Abstract Class?

| Interface | Abstract Class |
|---|---|
| Contract only | Partial implementation allowed |
| Multiple inheritance supported | Single inheritance only |
| No state (traditionally) | Can contain fields |
| Best for behavior definition | Best for shared functionality |

### Q26. Can a class implement multiple interfaces?

Yes, a class can implement multiple interfaces.

```csharp
public class Employee : ILogger, INotifier
{
}
```

---

## Constructors

### Q27. What is a Constructor?

A constructor is a special method that executes automatically when an object is created.

```csharp
public Employee() { }
```

### Q28. Types of Constructors in C#?

- Default Constructor
- Parameterized Constructor
- Copy Constructor (custom implementation)
- Static Constructor
- Private Constructor

### Q29. What is a Static Constructor?

Used to initialize static members. Runs only once per application domain.

```csharp
static Employee() { }
```

### Q30. What is Constructor Chaining?

Calling one constructor from another using `this`.

```csharp
public Employee() : this("Unknown") { }
```

---

## Keywords

### Q31. What is the `this` keyword?

Represents the current object instance.

```csharp
this.Name = name;
```

### Q32. What is the `base` keyword?

Used to access members of the parent class.

```csharp
base.CalculateSalary();
```

### Q33. What is a Sealed Class?

A sealed class cannot be inherited.

```csharp
public sealed class Utility { }
```

### Q34. What is a Sealed Method?

A method that cannot be overridden further.

```csharp
public sealed override void Display() { }
```

---

## Access Modifiers

### Q35. What are Access Modifiers?

Access modifiers define visibility and accessibility.

| Modifier | Accessibility |
|---|---|
| `public` | Everywhere |
| `private` | Same class |
| `protected` | Class + Derived Classes |
| `internal` | Same Assembly |
| `protected internal` | Derived Classes + Same Assembly |
| `private protected` | Same Assembly + Derived Classes |

### Q36. Difference between Public and Private?

| Public | Private |
|---|---|
| Accessible everywhere | Accessible only within class |
| Used for APIs | Used for internal data |

---

## Memory Management

### Q37. What is Garbage Collection?

Garbage Collection automatically reclaims memory occupied by unused objects. Managed by the .NET CLR.

### Q38. What are Generations in Garbage Collection?

- **Gen 0** → Short-lived objects
- **Gen 1** → Intermediate objects
- **Gen 2** → Long-lived objects

### Q39. What is IDisposable?

Used for releasing unmanaged resources.

```csharp
public class FileManager : IDisposable
{
    public void Dispose() { }
}
```

### Q40. Why should we use the `using` statement?

Ensures `Dispose()` is called automatically.

```csharp
using(var stream = new FileStream(...))
{
}
```

---

## Composition vs Inheritance

### Q41. What is Composition?

Composition represents a HAS-A relationship.

```csharp
public class Car
{
    private Engine engine; // Car HAS-A Engine
}
```

### Q42. Difference between Composition and Inheritance?

| Composition | Inheritance |
|---|---|
| HAS-A | IS-A |
| Flexible | Tight coupling |
| Preferred in modern design | Can lead to rigid hierarchy |

### Q43. Why is Composition often preferred over Inheritance?

- Reduces coupling
- Increases flexibility
- Simplifies maintenance
- Follows SOLID principles

---

## Dependency Injection

### Q44. What is Dependency Injection (DI)?

A design pattern where dependencies are supplied externally rather than created inside a class.

```csharp
public class EmployeeService
{
    private readonly ILogger _logger;

    public EmployeeService(ILogger logger)
    {
        _logger = logger;
    }
}
```

### Q45. Benefits of Dependency Injection?

- Loose coupling
- Better testing
- Easier maintenance
- Better scalability

---

## SOLID Principles

### Q46. What are SOLID Principles?

Five principles that help create maintainable and scalable software.

| Letter | Principle |
|---|---|
| S | Single Responsibility Principle |
| O | Open Closed Principle |
| L | Liskov Substitution Principle |
| I | Interface Segregation Principle |
| D | Dependency Inversion Principle |

### Q47. Explain Single Responsibility Principle (SRP).

A class should have only one reason to change. One class = One responsibility.

### Q48. Explain Open Closed Principle (OCP).

Software entities should be:
- Open for Extension
- Closed for Modification

New functionality should be added without changing existing code.

### Q49. Explain Liskov Substitution Principle (LSP).

Derived classes should be replaceable for their base classes without affecting correctness.

### Q50. Explain Interface Segregation Principle (ISP).

Clients should not be forced to depend on methods they do not use. Prefer smaller, focused interfaces.

### Q51. Explain Dependency Inversion Principle (DIP).

High-level modules should depend on abstractions, not concrete implementations.

```csharp
// Correct:
ILogger logger;

// Incorrect:
FileLogger logger;
```

---

## Senior-Level MNC Questions

### Q52. What is the difference between Association, Aggregation, and Composition?

| Relationship | Description |
|---|---|
| Association | General relationship between classes |
| Aggregation | Weak HAS-A (child can exist independently) |
| Composition | Strong HAS-A (child cannot exist without parent) |

### Q53. What is Loose Coupling?

A design where classes have minimal dependencies on each other. Usually achieved using:
- Interfaces
- Dependency Injection

### Q54. What is High Cohesion?

A class should contain closely related functionality and focus on a single responsibility.

### Q55. What are the benefits of OOP in enterprise applications?

- Code Reusability
- Maintainability
- Scalability
- Security
- Testability
- Extensibility
- Better Team Collaboration

### Q56. In a .NET enterprise application, which OOP concepts are used most frequently?

- Encapsulation through Properties
- Abstraction using Interfaces
- Dependency Injection
- Composition over Inheritance
- SOLID Principles
- Polymorphism through Service Implementations

These concepts form the foundation of modern ASP.NET Core MVC, ASP.NET Core Web API, Microservices, and enterprise-grade .NET applications.

---

**56 Questions & Answers covered.** Good luck with your interview! 🚀