---
layout: default
title: Naming
nav_order: 1
parent: C# Coding Guidelines
permalink: /csharp/coding/general
---

# General Guidelines

## Ternary Expressions
Ternary expressions are encouraged where appropriate, but should *never* be nested.

### ❌ Avoid
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
```cs
string result = condition ? "A" : "B";
```

### ❌ Avoid
```cs
string result = condition ? (nestedCondition ? "A" : "B") : "C";
```

### ✔️ Prefer
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

## Null Checking
Avoid using equality operators (`==`/`!=`) or `HasValue` (in the case of nullable value types) for null checks. Instead, make use of the `is` operator,
introducted in C# 7 for pattern matching expressions.

### ❌ Avoid
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
