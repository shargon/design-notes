<!-- markdownlint-enable -->
# NDX-DN10 - NEO Express Server Mode

- Author: Harry Pierson (harrypierson@ngd.neo.org)
- Status: Stub

## Abstract

This design note describes NEO Express server mode, which enables
NEO Express to be integrated into a variety of different development
environments suck as Visual Studio Code.  

## Raw Notes

- create command remains a stand alone command, but adds a --json flag
  to indicate it should return output as JSON for processing simplicity
- add new server command that is designed to work driven by an IDE like VSCode  
  - use same [base protocol as debug adapters](https://microsoft.github.io/debug-adapter-protocol/overview#base-protocol)
  - only support single session over stdin/out for now. Not sure multi-session
    over TCP will even be needed
  - server mode takes a single command line parameter - the path to the
    neo.express.json file. All commands sent to this server instance will be
    for this specific neo express instance
  - multiple running servers for the same neo-express.json file is not supported
    should investigate mechanism to ensure only one server instance is running
  - server mode will in turn be able to launch other instances of neo-express
    for running consensus nodes (both normal and checkpoint run). the Server
    mode process will communicate with consensus node processes using a similar
    JSON message based protocol running over stdin/out 
