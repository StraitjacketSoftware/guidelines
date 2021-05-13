---
layout: default
title: Naming Rules
nav_order: 1
parent: C# Style Guide
permalink: /csharp/styleguide/naming-guidelines
---

# Naming Rules
In general, we follow [Microsoft's C# naming guidelines](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/naming-guidelines), though there are a few differences.
{: .fs-6 .fw-300 }

## Capitalization
There are two appropriate ways to capitalise identifiers, depending on the usage:
- For parameters, local variables and private fields, use `camelCase`
- For all other uses, use `PascalCase`

Identifiers should never feature hyphens (-) or underscores (\_). Acronyms should be treated as a word, with only the first letter capitalized.

Interfaces and generic type parameters additionally should be prefixed with an `I` or a `T` as per the C# norm.

## Language
With the exception of `MonoBehaviour`, use US English spelling.

## Word Choice
Refer to Microsoft's C# [general naming conventions](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/general-naming-conventions), as well as the following documents:
- [Names of namespaces](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/names-of-namespaces)
- [Names of classes, structs and interfaces](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/names-of-classes-structs-and-interfaces)
- [Names of type members](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/names-of-type-members)
- [Naming parameters](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/naming-parameters)
- [Type parameter naming guidelines](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/generics/generic-type-parameters#type-parameter-naming-guidelines)
