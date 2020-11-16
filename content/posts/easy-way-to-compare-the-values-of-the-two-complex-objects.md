---
title: "Easy way to compare the values of the two complex objects"
date: 2020-11-15T19:45:09Z
draft: false
---
# Easy way to compare the values of the two complex objects

In C\#, Equals \(=\) check if the two objects are the same or the same instance. Often in unit tests,  you have to assert that the two objects have the same values in their object graphs. The easiest way is to serialize those objects in json or xml and compare the string.

```csharp
public static bool ValueEqual<T1, T2>(T1 expected, T2 actual)
{
    var expectedValues = JsonConvert.SerializeObject(expected);
    var actualValues = JsonConvert.SerializeObject(actual);

    return expectedValues == actualValues;
}
```

