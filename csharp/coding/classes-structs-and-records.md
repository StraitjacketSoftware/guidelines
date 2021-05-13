---
layout: default
title: When to Use Classes, Structs and Records
nav_order: 2
parent: C# Coding Guidelines
permalink: /csharp/coding/classes-structs-and-records
---

# When to Use Classes, Structs and Records
Not sure if your new type should be a class, struct or even a record?
{: .fs-6 .fw-300 }

It can be quite confusing when designing a type to decide whether it should be a class, a struct or a record (available from C# 9).
{: .fs-5 .fw-300 }

Does the data type you're designing respect all of [these rules](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/choosing-between-class-and-struct):
- It logically represents a single value, similar to primitive types (int, double, etc.)
- It has an instance size under 16 bytes
- It is immutable
- It will not have to be boxed frequently

If the answer to all of the above questions is **yes**, then your data type should be a `struct` (value type).

If you answered no to any of the above questions, then does your data type respect these rules:
- It is being defined with C# 9 or later
- It describes a value-like, preferably immutable state
- It will commonly be used in a unidirectional flow

If **yes**, then your data type should be a [`record`](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/record) (reference type).

Otherwise, your data type should be a `class` (reference type).
