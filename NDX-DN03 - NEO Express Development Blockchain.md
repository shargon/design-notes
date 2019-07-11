# NDX-DN03 - NEO Express Development Blockchain

- Author: Harry Pierson (harrypierson@ngd.neo.org)
- Status: Stub

## Abstract

This design note describes the features and design for NEO Express, a NEO
blockchain client application, optimized for development scenarios.

## Raw Notes

Primary use case is a single-node chain running locally on the developer's machine
but must also support multi-node, shared team deployment scenarios as well.

Basic operations (implemented in prototype) include:

- Create a new development blockchain. Developer can specify 1, 4 or 7 nodes.
  App creates an account for each node and node account + multi-sig account in
  an insecure wallet.
- create new standard accounts, stored in an insecure wallet. Use nicknames
  for accounts. node# and genesis are predefined nicknames.
- insecure wallets are clearly not for production use, but eliminates need for
  developers to remember passwords. Account nicknames makes it easier for developers
  to remember account info ("myaccount" vs "ANuupE2wgsHYi8VTqSUSoMsyxbJ8P3szu7")
- transfer tokens (NEO, GAS and/or NEP-5) between accounts
- claim gas for a specific account
- Smart contract deployment and invocation

Advanced Operations

- fast forward block chain in order to create GAS
- rollback block chain to a known snapshot for deterministic test execution
- blockchain state import/export for team collaboration + committing blockchain
  test state to version control system.

Tool Integration

- VS Code primary IDE target. Potentially support VS4Win and/or VS4Mac in the future but not now
- Invoke basic and advanced operations listed above via VS Code commands
- visual blockchain explorer for Express running as web view inside of IDE
