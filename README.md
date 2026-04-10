# ST10482781_PROG6221_Part1

ChatBotSecurity
================

A simple C# Console Chatbot that teaches basic cybersecurity topics and provides a small interactive UI.

Features
--------
- Conversational prompts and personalised responses (asks for user name)
- Plays a voice greeting WAV synchronously at startup (`Hello Welcome to the.wav`)
- ASCII logo and colored console UI
- Typing effect for bot responses
- Menu of 28 cybersecurity topics with short explanations

Requirements
------------
- .NET 10 SDK
- C# 14
- Visual Studio 2022+ / Visual Studio 2026 (tested in VS 2026)

Build & Run
-----------
From the project directory (`ChatBotSecurity`) you can build and run with the .NET CLI:

```
dotnet build
dotnet run --project ChatBotSecurity.csproj
```

Or open the solution in Visual Studio and run the project.

Voice greeting (WAV)
--------------------
The program uses `System.Media.SoundPlayer` which only supports WAV files. Place the `Hello Welcome to the.wav` file next to the executable or in the project root so the app can find and play it at startup.

To include the WAV in the build output automatically, add the following to `ChatBotSecurity.csproj` (or set the file property `Copy to Output Directory` to `Copy if newer` in Visual Studio):

```xml
<ItemGroup>
  <None Include="Hello Welcome to the.wav">
    <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
  </None>
</ItemGroup>
```

If you need MP3 support, reintroduce a player library such as NAudio and update the code accordingly.

Configuration
-------------
- The greeting file name is hard-coded in `Program.cs` at startup:

```
AudioPlayer.PlayExists = "Hello Welcome to the.wav";
```

Change that string to use another filename if desired.

Project structure and next steps
--------------------------------
Currently the app is implemented in a single file: `Program.cs`.
For better structure and maintainability (recommended for assignments), split the code into:

- `User.cs` – user state and validation
- `Chatbot.cs` – response logic and intent handling
- `AudioPlayer.cs` – audio playback helper
- `Program.cs` – application bootstrap and wiring

CI and GitHub
-------------
To meet CI requirements, create a GitHub repository and add a GitHub Actions workflow that builds the project. Example workflow file path:

`.github/workflows/dotnet.yml`

A minimal workflow that builds the project on `push`/`pull_request` to `main`:

```yaml
name: .NET
on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Setup .NET
        uses: actions/setup-dotnet@v4
        with:
          dotnet-version: '7.0.x' # adjust to your required SDK if needed
      - name: Restore and Build
        run: dotnet build --configuration Release
```

Commit suggestions
------------------
Make at least 6 commits as described in your assignment steps (example):
1. Initial project setup
2. Added voice greeting
3. Added ASCII art
4. Implemented user input
5. Added chatbot responses
6. Improved UI and validation

Notes
-----
- The included `AudioPlayer` uses `SoundPlayer` and falls back to a short `Console.Beep` if the WAV is not found or fails to play.
- The repo currently keeps everything in `Program.cs`. If you want I can refactor into separate files and add a CI workflow template.



