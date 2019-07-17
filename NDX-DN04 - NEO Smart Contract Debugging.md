# NDX-DN04 - NEO Smart Contract Debugging

- Author: Harry Pierson (harrypierson@ngd.neo.org)
- Status: Stub

## Abstract

This design note describes the features and design of the NEO Smart Contract Debugger.

## Raw Notes

- Not building a stand alone debugger like CoZ debugger tools. This reduces our development effort plus it
  integrates better into the developers existing workflow.
- VS Code is the primary IDE target. Potentially support VS4Win and/or VS4Mac in the future but not now.
- Leverage [Debug Adapter Protocol](https://microsoft.github.io/debug-adapter-protocol/). DAP is natively supported
  by VSCode. According to the [DAP Supporting Tools page](https://microsoft.github.io/debug-adapter-protocol/implementors/tools/)
  both [VS4Win](https://devblogs.microsoft.com/visualstudio/adding-support-for-debug-adapters-to-visual-studio-ide/)
  and VS4Mac are supported.
  - Details on VS4Mac support are scarce, but it's also the least important IDE target right now.
- NEO Debug Adapter built in C# since the production VM implementation is in C#. However, expectation is that
  the debugger will support debugging contracts written in any language that supports NEO contracts
- NEO compilers will need to be updated to generate debug info in addition to NeoVM byte code. At a minimum, this will include
  sequence points that map source code to byte code + function variable/argument information for variable inspection.
  For now, simply emitting this info from NEON in a simple, verbose JSON format. Longer term, we need to standardize on a
  compact and cross-language data format for this info, but not now
- Debugger will have two modes - "isolated" and "integrated"
  - Isolated mode is a stand alone instance of NeoVM where the blockchain interop services are emulated
  - Integrated mode means running in the context of a single node NEO Express developer blockchain. Note, since the debugger
    needs to pause the contract during execution, only single-node Express instances will support debugging.
  
## Links

- [Managed implementation of the VS Code Debug Protocol](https://www.nuget.org/packages/Microsoft.VisualStudio.Shared.VsCodeDebugProtocol)
  no source for some reason.
- [Sample Debug Adapter](https://github.com/microsoft/VSDebugAdapterHost/tree/master/src/sample/SampleDebugAdapter)
