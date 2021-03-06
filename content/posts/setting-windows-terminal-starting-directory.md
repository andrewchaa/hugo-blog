---
title: "Setting Windows Terminal Starting Directory"
date: 2020-11-15T19:45:09Z
draft: false
---
# Setting Windows Terminal Starting Directory

Since the first non-preview version, I have been using [Windows Terminal](https://github.com/Microsoft/Terminal). You can install it from the [Microsoft Store](https://aka.ms/terminal). Or via CLIs

**Via Windows Package Manager CLI \(aka winget\)**

[winget](https://github.com/microsoft/winget-cli) users can download and install the latest Terminal release by installing the `Microsoft.WindowsTerminal` package:

```text
winget install --id=Microsoft.WindowsTerminal -e
```

**Via Chocolatey \(unofficial\)**

[Chocolatey](https://chocolatey.org/) users can download and install the latest Terminal release by installing the `microsoft-windows-terminal` package:

```text
choco install microsoft-windows-terminal
```

To upgrade Windows Terminal using Chocolatey, run the following:

```text
choco upgrade microsoft-windows-terminal
```

One thing that bugged me was it opens from the default directory, C:\Users\:username. I create c:\dev directory and put all my code in there, so it would be very handy for me if it opens from c:\dev.

Simple. press ctrl + ,

Then it will open settings.json. You can add "startingDirectory" in the profiles. You can find the documentation from ms [terminal-documentation](https://aka.ms/terminal-documentation)

```bash
"profiles":
{
    "defaults":
    {
        // Put settings here that you want to apply to all profiles.
        "startingDirectory": "c:\\dev"
    },
    "list":
    [
        {
            // Make changes here to the powershell.exe profile.
            "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
            "name": "Windows PowerShell",
            "commandline": "powershell.exe",
            "hidden": false
        },
```

