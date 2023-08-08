---
layout: post
title: "Generics in .NET"
categories: Miscellaneous
---
# Generics in .NET

Generics are a powerful feature of .NET that allow for the creation of reusable code that can work with a variety of data types. In this post, we'll explore what generics are, when and why to use them, examples of generics, and covariance and contravariance with examples.
## What are generics?

Generics are a way to define a class, structure, interface, or method where in we can defer the specification of one or more types used by them until the class or method is declared and instantiated by client code  . Many times, we need to define a class or a method (i.e. a behavior) that is common for various types. In these cases, rather than defining multiple  similar classes or methods that have the same behavior except for the type they work on, we can define a generic class or method. We can then use this generic class or method with different datatypes, that share the behavior. This helps in preventing duplicate code, centralizing the logic, ease of testing, removes the cost or risk of runtime casts of types or boxing operations. This also makes your code more flexible and reusable.

## When and why to use generics

Generics are particularly useful when you need to write code that can work with multiple data types. For example, if you're writing a collection class, you could use generics to allow the collection to work with any data type. Generics can also improve the performance of your code by reducing the need for type conversions.

## Examples of generics

Let's take a look at a simple example of a generic class. The following code defines a generic Stack class that can work with any data type:

```csharp
public class Stack<T>
{
    private List<T> items = new List<T>();

    public void Push(T item)
    {
        items.Add(item);
    }

    public T Pop()
    {
        T item = items[items.Count - 1];
        items.RemoveAt(items.Count - 1);
        return item;
    }
}

```

In this example, the type parameter T is used to specify the type of the items in the stack. When you create an instance of the Stack class, you specify the data type you want to use.


> [!NOTE] About type parameter T
> Type parameter T is used in several locations where a concrete type would ordinarily be used to indicate the type of the item stored on the stack. It is used in the following ways:
> - As the type of a method parameter in the `Push` method.
> - As the return type of the `Pop` method.
> - As the type on the `Stack` class.

## Constraints
The type parameters in generic methods, classes, interfaces, delegates can be constrained, if required, using constraining rules.
Here is an example of constraint in a generic class definition
```csharp
public class Test<T> where T : struct
{
}
```

In the above example, we constrained the type that can be used with `Test` generic class to be `struct`.

Multiple constraints can be added to one or more type parameters

```csharp
class Base { }
class Test<T, U>
    where U : struct
    where T : Base, new()
{ }
```

In the above example:
- Type parameter U is constrained to be a struct
- Type parameter T is constrained to be of a type deriving from Base and one that has a public parameter-less constructor.
## Covariance and contravariance

Covariance and contravariance are advanced features of generics that allow you to use a derived data type in place of a base data type, or a base data type in place of a derived data type. This can be useful in certain scenarios, such as when working with collections.

Here's an example of covariance:

```csharp
IEnumerable<string> strings = new List<string>();
IEnumerable<object> objects = strings; // covariance

```

In this example, we have a list of strings that we're assigning to a variable of type IEnumerable<object>. This is possible because string is derived from object.

Here's an example of contravariance:

```csharp
Action<object> printObject = (object o) => Console.WriteLine(o);
Action<string> printString = printObject; // contravariance

```

In this example, we have a method that takes an object as a parameter and prints it to the console. We're assigning this method to a variable of type Action<string>. This is possible because string is a derived type of object.

## Conclusion

- Use generic types to maximize code reuse, type safety, and performance.
- The most common use of generics is to create collection classes.
- You can create your own generic interfaces, classes, methods, events, and delegates.
- Generic classes may be constrained to enable access to methods on particular data types.
- Information on the types that are used in a generic data type may be obtained at run-time by using reflection.

