# NDX-DN05 - NEO Toolkit for .NET

- Author: Harry Pierson (harrypierson@ngd.neo.org)
- Status: Stub

## Abstract

This design note describes the features and design of the libraries and tools
used by .NET developers to target the NEO platform.

## Raw Notes

- .NET Libraries distributed via NuGet. Common tasks across in/on/off chain
  development should have similar if not identical programming models as per UPM
  Focus on in-chain (aka smart contract) and off-chain scenarios to start.
- templates for NEO projects distributed via NuGet. Templates include tasks
  (preferably [inline tasks](https://docs.microsoft.com/en-us/visualstudio/msbuild/msbuild-inline-tasks?view=vs-2019))
  for running NEON as part of the build process
- NEON compiler distributed as .NET global tool. Potentially re-write NEON compiler.
  At a minimum, NEON compiler needs to emit information needed by debugger and support
  compiling .NET Standard assemblies -> NeoVM)
- on/off chain apps are basically standard .NET apps (cmd line, GUI, mobile, etc)
  that use a NEO library distributed via NuGet. simply dotnet add package and you're done.
  - Note, we already can do this for on-chain development by simply adding the neo package via nuget.
    However, I'm thinking that we could provide a better and more modular framework for on-chain developers
- in chain apps have custom inner loop:
  1. New contract: "dotnet new neocontract"
  2. Edit contract: This is just the standard VSCode editing experience. No extension needed
  3. Compile contract: neocontract template includes custom (inline) build tasks in proj file
     to invoke NEON during build
  4. Debug Contract: Run the contract in the NEO contract Debugger. VSCode may support extension
     commands for configuring launch.json file with relevant info (isolated / integrated)
