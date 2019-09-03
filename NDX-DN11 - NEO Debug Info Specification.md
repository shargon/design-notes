<!-- markdownlint-enable -->
# NDX-DN10 - NEO Express Server Mode

- Author: Harry Pierson (harrypierson@ngd.neo.org)
- Status: Stub

## Abstract

This design note describes the debug information format used by
the [NEO Smart Contract Debugger](NDX-DN04%20-%20NEO%20Smart%20Contract%20Debugging.md).
This information will be generated by smart contract compilers
such as [NEON](https://github.com/neo-project/neo-devpack-dotnet)
or [neo-boa](https://github.com/CityOfZion/neo-boa).

The current version of the debugger uses a temporary debug info
format generated by a
[fork of the NEON compiler](https://github.com/neo-project/neo-devpack-dotnet/tree/dehvawk/neon-de).
This format was has not been peer reviewed or optimized for size or performance.
There is no expectation that the current format will be the final format.
At a minimum, the format needs to be improved to eliminate redundant information
that bloats the file size. Realistically, representatives from other smart
contract compiler projects needs to be given an opportunity to provide input
so that the final format can be used across the various languages in the NEO
ecosystem.