# NDX-DN04 - NEO Smart Contract Debugging

- Author: Harry Pierson (harrypierson@ngd.neo.org)
- Status: Stub

## Abstract

This design note describes the features and design of the NEO Smart Contract Debugger.

## Raw Notes

- VS Code is the primary IDE target. Potentially support VS4Win and/or VS4Mac in the future but not now.
- Not building a stand alone debugger like CoZ debugger tools. This reduces our development effort plus it
  integrates better into the developers existing workflow.
- Leverage [Debug Adapter Protocol](https://microsoft.github.io/debug-adapter-protocol/). Natively supported
  by VSCode, I believe DAP is also supported by VS4win.
- Need to support what I'm currently calling "isolated" and "integrated" mode. Integrated mode means running
  in the context of the NEO Express developer blockchain. Isolated mode is a stand alone instance of NeoVM
  where the blockchain interop services are emulated
- Will need NEO compilers to generate debug info in addition to NeoVM byte code. At a minimum, this will include
  sequence points that map source code to byte code + function variable/argument information for variable inspection.
  Eventually need to standardize on a data format for this info, but that can be longer term
