---
layout: default
title: Whitespace
nav_order: 2
parent: C# Formatting Guidelines
permalink: /csharp/formatting/whitespace
---

# Whitespace

## Indentation
Indentation should be in blocks of **4 spaces**. *We **never** use tabs.*

In the case of method definitions and calls where arguments do not all fit on line, they should be broken up onto multiple lines, with each subsequent line
aligned with the first argument. If there is not enough room for this, use a 4 space indent instead.

## Character Limit per Line
A line should never exceed **150 characters** in length.

## Braces
Braces should always be separated out onto their own line as per the C# convention. The _only_ exception is when initializing an object or collection via [initializer syntax](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/object-and-collection-initializers), and only in the case of assigning a single property
or a very simple, short list.

**There are no such thing as optional braces.** Conditional statements are *always* required to be enclosed in braces.

## Spaces
There should be one space after `if`/`for`/`while` etc. keywords, and after commas.

There should be one space between an operator and each of its operands, with the exception of unary operators such as `!`.

## Vertical Whitespace
There should be only one field or variable declaration per line.

There should be exactly one blank line between methods and property declarations. Property declarations with a backing field do not require a space between the
backing field and the property, but the backing field must be declared on the line immediately preceding the property.

Whitespace within code blocks should separate logical functionality, but if you find there are many sections in a method, you should likely consider refactoring
to split the method into smaller pieces.
