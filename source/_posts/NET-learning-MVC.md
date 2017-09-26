---
title:  .NET学习之MVC指令学习
category: NET
tags:
  - .NET
  - MVC
date: 2017-04-01 00:00:00
---
Usage:

```.net
dotnet [host-options] [command] [arguments] [common-options]
```

  <!-- more -->

> Arguments:

| parameter | content |
|:-------|:-------|
|  [command]          |  The command to execute
|  [arguments]        |  Arguments to pass to the command
|  [host-options]     |  Options specific to dotnet (host)
|  [common-options]   |  Options common to all commands

> Common options:

| parameter | content |
|:-------|:-------|
|  -v or --verbose       |  Enable verbose output
|  -h or --help          |   Show help

> Host options (passed before the command):

| parameter | content |
|:-------|:-------|
|  -d or --diagnostics   |  Enable diagnostic output
|  --version          |  Display .NET CLI Version Number
|  --info             |  Display .NET CLI Info

> Commands:

| parameter | content |
|:-------|:-------|
|  new       |  Initialize .NET projects.
|  restore   |  Restore dependencies specified in the .NET project.
|  build     |  Builds a .NET project.
|  publish   |  Publishes a .NET project for deployment (including the runtime).
|  run       |  Compiles and immediately executes a .NET project.
|  test      |  Runs unit tests using the test runner specified in the project.
|  pack      |  Creates a NuGet package.
|  migrate   |  Migrates a project.json based project to a msbuild based project.
|  clean     |  Clean build output(s).
|  sln       |  Modify solution (SLN) files.

> Project modification commands:

| parameter | content |
|:-------|:-------|
|  add        |  Add items to the project
|  remove     |  Remove items from the project
|  list       |  List items in the project

> Advanced Commands:

| parameter | content |
|:-------|:-------|
|  nuget      |  Provides additional NuGet commands.
|  msbuild    |  Runs Microsoft Build Engine (MSBuild).
|  vstest     |  Runs Microsoft Test Execution Command Line Tool.
