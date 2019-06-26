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

## Developing for the Smart Economy

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

### Developer Tools

#### Go where the developers already are



#### Make it easy to aquire the libraries and tools needed for Smart Economy development


It must be easy for developers to aquire the t

Most language ecosystems have a package management system for 

* NPM for JavaScript
* NuGet for .NET
* VS Marketplace for Visual Studio Code

#### Make it easy to get started

new project templates

#### Personal Blockchain

#### Debugger

#### Development Lifecycle


### Guidance

#### Getting Started Guidance

#### Advanced Guidance





As per the official whitepaper[^1], NEO integrates into existing
mainstream developer ecosystems.

-   New project templates, including new smart contracts and new dApp
    templates

-   

### A Blockchain Optimized Development and Testing

Today, NEO provides two clients to connect to a blockchain instance:
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

NEO Express is not designed for creating or managing a production
blockchain instance where the nodes are running on separate physical
machines. Automating the creation of a production private blockchain
instance is an important scenario in general, but it\'s not a developer
scenario for NEO Express.

While NEO Express will be further detailed in a future design note, here
is a quick summary of its capabilities:

-   A developer can quickly create a new blockchain instance on their
    machine via the command line. No manual wallet creation or hand
    editing of json files required.

-   A developer can have multiple NEO Express blockchains on their
    machine. Developers often work on multiple projects at a time. Even
    individual projects may need multiple development blockchains for
    different usage scenarios (front end vs. back end, dev vs. test,
    etc). These different blockchains can be running on the local
    machine at the same time (subject to available machine resources)

-   Developers can create wallet accounts for use on NEO Express
    blockchains. These wallet accounts will have user friendly names
    like "Alice" and "Bob" instead of base-58 encoded account hashes
    like "AJzoeKrj7RHMwSrPQDPdv61ciVEYpmhkjk". As these wallet accounts
    are designed for dev scenarios, they can optionally be created
    without a password.

-   Developers can transfer assets - NEO, GAS and NEP-5 -- between
    wallet accounts easily and quickly. This includes transferring
    genesis block NEO of a newly created blockchain instance to a
    standard wallet account. Wallet accounts can earn and claim GAS as
    they would on MainNet or TestNet.

-   Developers can easily change the rate at which a given NEO Express
    blockchain instance creates blocks. To simulate the conditions of
    MainNet, it can run at 15 seconds per block. To facilitate inner
    loop development and the creation of GAS, it can run as fast as 1
    second per block.

-   Developers can snapshot, rollback, import and export the state of
    the blockchain. Snapshot and Rollback allows for repeatable
    automated testing. Import/export is similar to offline packages of
    blockchain data NGD makes available to speed up network
    synchronization on MainNet and TestNet

-   Developers can explore the state of the blockchain, inspecting
    individual accounts, blocks and transactions.

NEO Express is a command line tool for developers to use in the
development and testing of NEO Smart Contracts. It builds on the same
core NEO platform as NEO-CLI and NEO-GUI while providing unique
capabilities specific to the developer scenario

### Developer Tool Acquisition

[^1]: NEO Whitepaper <https://docs.neo.org/en-us/whitepaper.html>

[^2]: Source: Stack Overflow 2018 Developer Survey, Most Popular
    Development Environments
    <https://insights.stackoverflow.com/survey/2018/#technology-_-most-popular-development-environments>
