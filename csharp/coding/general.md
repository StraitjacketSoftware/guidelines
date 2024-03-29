---
layout: default
title: General Guidelines
nav_order: 1
parent: C# Coding Guidelines
permalink: /csharp/coding/general
---

# General Guidelines
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## Ternary Expressions
[Ternary expressions](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/conditional-operator) are encouraged where appropriate, but should *never* be nested.

### ❌ Avoid
{: .no_toc .text-delta }
```cs
string result;
if (condition)
{
    result = "A";
}
else
{
    result = "B";
}
```

### ✔️ Prefer
{: .no_toc .text-delta }
```cs
string result = condition ? "A" : "B";
```

### ❌ Avoid
{: .no_toc .text-delta }
```cs
string result = condition ? (nestedCondition ? "A" : "B") : "C";
```

### ✔️ Prefer
{: .no_toc .text-delta }
```cs
string result;
if (condition)
{
    result = nestedCondition ? "A" : "B";
}
else
{
    result = "C";
}
```

However, starting with C# 8, prefer [switch expressions](#switch-statements-and-expressions):
```cs
string result = condition switch
{
    true when nestedCondition => "A",
    true                      => "B",
    false                     => "C"
};
```

## Null Checking
Avoid using equality operators (`==`/`!=`) or `HasValue` (in the case of nullable value types) for null checks. Instead, make use of the [`is` operator](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/is),
introducted in C# 7 for pattern matching expressions.

### ❌ Avoid
{: .no_toc .text-delta }
```cs
int? number = 42;
if (number != null)
{
    // ...
}

if (number.HasValue)
{
    // ...
}
```

### ✔️ Prefer
{: .no_toc .text-delta }
```cs
int? number = 42;
if (number is int n)
{
    // n has now been cast from an int? to an int with the value of 42
    // ...
}
```

Starting with C# 9, we also have access to the `not` operator:
```cs
if (value is not null)
{
    // ...
}
```

## Switch Statements and Expressions
Switch statements should be preferred over `if`-`else if`-`else` statements wherever possible.

### ❌ Avoid
{: .no_toc .text-delta }
```cs
if (number == 1)
{
    // ...
}
else if (number == 2)
{
    // ...
}
else if (number == 3)
{
    // ...
}
else
{
    // ...
}
```

### ✔️ Prefer
{: .no_toc .text-delta }
```cs
switch (number)
{
    case 1:
        // ...
        break;
    case 2:
        // ...
        break;
    case 3:
        // ...
        break;
    default:
        // ...
        break;
}
```

However, where possible, prefer [switch expressions](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/switch-expression) over switch statements. Switch expressions are available starting from C# 8, and are useful when assigning to a variable or returning from a method based on simple [pattern mattern expressions](https://docs.microsoft.com/en-us/archive/msdn-magazine/2019/may/csharp-8-0-pattern-matching-in-csharp-8-0):

### ❌ Avoid
{: .no_toc .text-delta }
```cs
string result;
switch (someEnum)
{
    case MyEnum.None:
        result = "No selection.";
        break;
    case MyEnum.Action:
        result = "Action selected.";
        break;
    case MyEnum.Choice:
        result = "Choice selected.";
        break;
    case MyEnum.Message:
        result = "Message selected.";
        break;
}
```

### ✔️ Prefer
{: .no_toc .text-delta }
```cs
string result = someEnum switch
{
    MyEnum.None     => "No selection.",
    MyEnum.Action   => "Action selected.",
    MyEnum.Choice   => "Choice selected.",
    MyEnum.Message  => "Message selected.",
    _               => throw new InvalidOperationException() // _ is analagous to the default case in a switch statement
}
```

## String Concatenation
[String interpolation](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/tokens/interpolated) should always be preferred over using the `+` operator or the `string.Format()` method wherever possible.

### ❌ Avoid
{: .no_toc .text-delta }
```cs
string name = firstName + " " + lastName;
```
```cs
string name = string.Format("{0} {1}", firstName, lastName);
```

### ✔️ Prefer
{: .no_toc .text-delta }
```cs
string name = $"{firstName} {lastName}";
```

## Variable Declaration
Avoid use of the `var` keyword, except where the type being assigned is obvious without any additional context.

### ❌ Avoid
{: .no_toc .text-delta }
```cs
var users = Database.GetUsers();
```

### ✔️ Prefer
{: .no_toc .text-delta }
```cs
List<User> users = Database.GetUsers();
```
```cs
var users = new List<User>();
```

Starting with C# 9, it is also possible to use the following syntax when constructing a new object, which is preferred where applicable:
```cs
List<User> users = new();
```

## Object Initialization
When initializing an object, avoid assigning individual properties via multiple statements, instead preferring [object and collection initializer](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/object-and-collection-initializers) syntax.

### ❌ Avoid
{: .no_toc .text-delta }
```cs
Cat cat = new Cat();
cat.Age = 10;
cat.Name = "Fluffy";
```

### ✔️ Prefer
{: .no_toc .text-delta }
```cs
Cat cat = new Cat
{
    Age = 10,
    Name = "Fluffy"
}
```

### ❌ Avoid
{: .no_toc .text-delta }
```cs
List<int> numbers = new List<int>();
numbers.Add(1);
numbers.Add(2);
```

### ✔️ Prefer
{: .no_toc .text-delta }
```cs
List<int> numbers = new List<int> { 1, 2, 3 }
```
```cs
Dictionary<int, string> numberDictionary = new Dictionary<int, string>
{
    [7] = "seven",
    [9] = "nine",
    [13] = "thirteen"
}
```
