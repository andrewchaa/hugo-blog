---
title: "Prettify JSON with C#"
date: 2020-11-15T19:45:09Z
draft: false
---
# Prettify JSON with C#

Formating JSON is easy peasy with javascript. There are so many different  flavours of libraries. Yet, it's not true with C\#. The other day, I encountered a use case where I had to prettify JSON in C\#.

Interestingly, [JSON.Net](https://www.newtonsoft.com/json) supported the feature already. The following's the code.

```csharp
var content = Encoding.UTF8.GetString(message.Body);
var beautified = JToken.Parse(content).ToString(Formatting.Indented);
```

