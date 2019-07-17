<!-- markdownlint-enable -->
# NDX-DN02 - NEO Unified Programming Model

- Author: Harry Pierson (harrypierson@ngd.neo.org)
- Status: Stub

## Abstract

This design note describes the design of NEO's unified programming
model - a single programming model for off-chain, on-chain and in-chain
code in a decentralized blockchain application.

# Raw Notes

Need to identify types and operations used across in/on/off chain development

- [RPC API Docs](https://docs.neo.org/en-us/node/cli/latest-version/api.html)
- [Smart Contract Reference](https://docs.neo.org/en-us/sc/reference/api.html)

> Note, today we expose pure request/response APIs for off-chain access.
> However, we could also expose WebSocket APIs to off chain clients, so that
> we could further unify the programming models.

Types

- UInt160 and UInt256
- BigDecimal
- Fixed8
- Block
- Transaction

Operations

- get blocks
- Invoke smart contracts
- access oracle
- transfer asset (2.x only - 3.x uses smart contracts for all asset management)
