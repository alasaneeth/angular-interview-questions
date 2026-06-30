# C# Generics and Collections — Interview Questions Guide

## Section 1 — Basic C# Generics

### Q1. What are Generics in C#?

Generics allow you to create classes, methods, interfaces, and delegates with a placeholder for the data type, enabling type safety and code reuse.

```csharp
List<int> numbers = new List<int>();
```

**Advantages:**
- Type safety
- Code reuse
- Better performance
- Compile-time checking

### Q2. Why do we use Generics?

**Before Generics:**

```csharp
ArrayList list = new ArrayList();
list.Add(10);
list.Add("Hello");
```

**Problems:**
- No type safety
- Runtime errors
- Boxing/Unboxing

**With Generics:**

```csharp
List<int> list = new List<int>();
list.Add(10);
```

**Benefits:**
- Strong typing
- Better performance
- IntelliSense support

### Q3. What problems do Generics solve?

- Eliminates casting
- Eliminates boxing/unboxing
- Improves performance
- Improves code readability
- Provides compile-time validation

### Q4. Difference between Generic and Non-Generic Collections?

| Generic | Non-Generic |
|---|---|
| Type Safe | Not Type Safe |
| No Boxing | Boxing Required |
| Compile-time checking | Runtime checking |
| Faster | Slower |
| Namespace: `System.Collections.Generic` | Namespace: `System.Collections` |

### Q5. What is type safety?

Only one data type can be stored.

```csharp
List<int> list = new List<int>();
list.Add(10);
list.Add("Hello"); // Compile Error
```