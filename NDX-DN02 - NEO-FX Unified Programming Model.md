<!-- markdownlint-enable -->
# NDX-DN02 - NEO-FX Unified Programming Model

- Author: Harry Pierson (harrypierson@ngd.neo.org)
- Status: Stub

## Abstract

This design note describes the design of NEO's unified programming
model - a single programming model for Remote, Node and Contract SDKs
in a decentralized blockchain application.

# Raw Notes

Need to identify types and operations used for Remote, Node and Contract development.

- [RPC API Docs](https://docs.neo.org/en-us/node/cli/latest-version/api.html)
- [RPC wrapper code in NEO 3.0](https://github.com/neo-project/neo/pull/850)
- [Smart Contract Reference](https://docs.neo.org/en-us/sc/reference/api.html)

> Note, today we expose pure request/response APIs for remote access.
> However, we could also expose WebSocket APIs to remote clients, so that
> we could further unify the programming models.

Fundamental Types

- UInt160 and UInt256
- BigDecimal
- Fixed8

Domain Models

- Block
- Transaction

Service Abstractions

- get blocks
- Invoke smart contracts
- access oracle
- transfer asset (2.x only - 3.x uses smart contracts for all asset management)
