---
layout: default
title: Public Fields
nav_order: 3
parent: C# Coding Guidelines
permalink: /csharp/coding/public-fields
---

# When to Use Public Fields
Wherever possible, we stick to Microsoft's [design guidelines](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/field) when it comes to fields.
{: .fs-6 .fw-300 }

We agree with these guidelines that the principle of encapsulation is one of the most important aspects of object-oriented design.
As such, only members that _need_ to be `public` should be `public`.

**Instance fields never need to be `public`.**

The only fields that should be `public` are constant or static read-only fields used for defining default object states (e.g. `Vector3.zero`), 

For the purpose of exposing data to consumers of the type, you should define a `property` with a `get` accessor that forwards to the field (or an auto-implemented property).
Don't expose the `field` directly.

## Unity
The common convention when developing a custom `MonoBehaviour` in Unity is to use `public` fields for anything you wish to expose in the Unity inspector.

However, *the vast majority of the time, these fields should be private*.

The Unity inspector respects the `SerializeField` attribute. When used to decorate a `private` field, the field will be accessible and editable in the inspector:

```cs
[SerializeField]
private string text;
```

Available from C# 7.3 and up, it is now possible to target the backing field of auto-implemented properties, irrespective of the accessibility of the `set` accessor:
```cs
[field: SerializeField]
public string Text { get; private set; }
```

As such, *the vast majority of fields you wish to expose in the Unity inspector should actually be properties.*
