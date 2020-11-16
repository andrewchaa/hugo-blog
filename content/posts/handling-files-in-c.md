---
title: "Handling files in c#"
date: 2020-11-15T19:45:09Z
draft: false
---
# Handling files in c#

So often I have to read and write files, yet I forget how to do it. This is for me to remember.

You can use `Directory.GetFiles` that searches subdirectories for  you.\([https://stackoverflow.com/questions/9830069/searching-for-file-in-directories-recursively/9830116](https://stackoverflow.com/questions/9830069/searching-for-file-in-directories-recursively/9830116)\)

```csharp
string[] files = Directory.GetFiles(sDir,
  "*.xml",
  SearchOption.AllDirectories);
```

