---
title: "Fail the deserializatioin of JSON string if any expected properties don't exist"
date: 2020-11-15T19:45:09Z
draft: false
---
# Fail the deserializatioin of JSON string if any expected properties don't exist

I can simply put \[Required\] attribute in ASP.NET Core. On my personal project, I use AWS Lambda and the SDK doesn't have that feature out of the box.

Json.NET has another handy attribute, \[JsonObject\(ItemRequired = Required.Always\)\]. It makes every property of the class mandatory

```csharp
[JsonObject(ItemRequired = Required.Always)]
public class UpdateWarrantyRequest
{
    public int WarrantyYear { get; set; }
}
```

Then I can catch the exception and handle it.

```csharp
public static class JsonExtensions
{
    public static OperationResult<T> To<T>(this string payload)
    {
        try
        {
            return new OperationResult<T>(HttpStatusCode.OK,
                JsonConvert.DeserializeObject<T>(payload));
        }
        catch (Exception)
        {
            var errorMessage = $"Failed in deserializing the payload:\n {payload}";
            Console.WriteLine(errorMessage);
            return new OperationResult<T>(HttpStatusCode.BadRequest, errorMessage);
        }
    }
}

```

