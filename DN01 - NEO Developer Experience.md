<!-- markdownlint-enable -->
# DN01 - NEO Developer Experience

- Author: Harry Pierson (harrypierson@ngd.neo.org)
- Status: Draft

## Abstract

This design note describes the goals and guiding principles of a world-class
experience for developers targeting the NEO platform. This note is intended to
be high level and aspirational. Further design notes will specify in detail how
individual capabilities will be implemented.

## Overview

> "Make the impossible possible, the possible easy, the easy elegant." - Moshé Feldenkrais

Broad adoption is critical for  NEO to deliver on the
[Smart Economy vision](https://docs.neo.org/en-us/whitepaper.html#neo-design-goals-smart-economy)
outlined in the [NEO Whitepaper](https://docs.neo.org/en-us/whitepaper.html).
As the tech industry has seen play out many times, developers are critical to platform
adoption.

Developers need two - somewhat contradictory - things

- Make it powerful
- Make it easy

Like all humans, developers want things to be easy. However, developers are also
driven by challenge. This challenge may be finanical in nature ("I want to make money
on what I create") but it may not.

Core NEO platform is focused on building the powerful capabilities for developers
to deliver Smart Economy solutions. The NEO Developer Experience is focused on
making the Smart Economy develpment as easy as possible.

- first principles

## Developing for the Smart Economy

## Blockchain dApp Architecture

Management of digital assets is a critical enabling feature of the Smart Economy.
The NEO Whitepaper identifies blockchain technology as the critical infrastructure needed to enable digital assets

The NEO blockchain is a peer-to-peer network topology running across a
decentralized networks of machines, 

The NEO blockchain utilizes two strategies for communication between nodes in
the network. 



The first strategy is a connection-oriented, full-duplex protocol running on top of TCP and/or WebSockets.


https://docs.neo.org/en-us/network/network-protocol.html

 Nodes using this protocol typically
establish long-lived connections to multiple other nodes in the network. These
long-lived connections allow for efficient communication between consensus nodes
and they enable changes to the system - for example, a new block being created -
to be broadcast across the entire network. Nodes using this protocol typically have
a full copy of the blockchain data local to the node. 

The second strategy for communication within the blockchain network is a stateless,
request-response protocol. This protocol leverages [JSON-RPC](https://www.jsonrpc.org/specification)
on top of HTTP. Unlike the 









| off-chain  | on-chain  | in-chain       |
| --         | --        | --             |
| RPC client / "lite" node | P2P Client / full node | smart contract |

Developing for the Smart Economy involves multiple different types of
projects.

- Decentralized Apps (also known as dApps) are apps that run across a
  peer-to-peer network of machines. There are many types of
  decentralized apps, but the primary focus of this design note is
  blockchain apps (as opposed to say BitTorrent apps).

- Smart Contracts are piec es of backend logic that are deployed into
  the blockchain. They can be invoked either by members of the
  blockchain network (perhaps proxying an invocation coming from
  outside the network), by other smart contracts or in response to
  pre-programmed condition in the blockchain itself.

## Scenarios

### Work with the developer ecosystem I already know.

As per the official whitepaper, NEO is designed to integrate into existing
mainstream developer ecosystems. 

### Make it easy to get started.

It must be easy for developers to aquire the t

Most language ecosystems have a package management system for 

* NPM for JavaScript
* NuGet for .NET
* VS Marketplace for Visual Studio Code


new project templates


### A Blockchain optimized development and testing

Today, NEO provides two official clients to connect to a blockchain instance:
neo-cli and neo-gui. These clients can connect MainNet, TestNet or can
be used to run a private blockchain instance. These clients are used to
run consensus nodes and by real end users to transfer assets on the
MainNet. As such, they must be optimized for security and other
production usage scenarios.

NEO Express is a new NEO blockchain client, optimized for development
scenarios. It will be built on the same NEO platform core as neo-cli and
neo-gui are, ensuring that developer's code will run the same on MainNet
as it does in their development environment. NEO Express will run on the
developer's local machine, using as few resources as needed to host the
blockchain instance.

* Blockchain Explorer integrated into tool

### Debug my smart contracts

### Manage My dApp for the Entire Application Lifecycle

Development doesn't end with deployment. In many ways, deploment represents the start of the real work

* deployment to mainnet 
* Monitoring a deployed dApps
* Associating events in remote clients, on chain clients and smart contracts

### Give me guidance

#### Getting Started Guidance

#### Advanced Guidance

#### Show me what a blockchain can do

sample app













