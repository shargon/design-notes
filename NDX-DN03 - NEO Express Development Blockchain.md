<!-- markdownlint-enable -->
# NDX-DN03 - NEO Express Development Blockchain

- Author: Harry Pierson (harrypierson@ngd.neo.org)
- Status: Draft

## Abstract

This design note describes the features and design for NEO Express, a NEO
blockchain client application, optimized for development scenarios.

## Overview

Today, NEO provides two official client applications for blockchain network
nodes: neo-cli and neo-gui. These clients can connect MainNet, TestNet or can
be used to run a private blockchain instance. These clients are used to
run consensus nodes and by real end users to transfer assets on the
MainNet. As such, neo-cli and neo-gui must be optimized for security and other
production usage scenarios.

neo-express is a new NEO blockchain client application, optimized for development
scenarios. It will be built on the same NEO platform core as neo-cli and
neo-gui are, ensuring that developer's code will run the same on MainNet
as it does in their development environment. NEO Express will support multiple
deployment scenarios, from a single node blockchain running on a developer's
machine to a multi node blockchain shared by a development team.

Similar to neo-cli, neo-express is a command line tool. However, unlike neo-cli,
most operations for neo-express will be short lived. This will enable neo-express
to be scriptable by developers as needed. The exception to these short lived
operations is running a consensus node of a private blockchain instance. The running
blockchain instance can be started and shutdown at the developers whim, but operations
like asset transfer and smart contract execution require the blockchain instance
to be running.

neo-express will be available for both NEO 2 and NEO 3. Currently, the NEO 2
version of neo-express has been the focus while NEO 3 is stabilized for the first
preview release. Once the initial preview release of NEO 3 has been deployed,
porting will begin to neo-express on top of the NEO 3 code base.

> There will likely be two separate versions of neo-express, one to support NEO
> 2 and one for NEO 3. However, if it is possible to support both versions with a
> single tool via dynamic assembly loading, that would be a preferable solution.

## Blockchain Instance Management

### neo-express create

Creating a block chain instance requires creating a wallet for each consensus node,
along with a multi-signature contract to manage the genesis assets. neo-express
provides a simple create command to make creating a new blockchain instance nearly
painless.

All the information about the blockchain - the consensus nodes, standard wallets
and smart contracts - lives in a single JSON file. By default, this file is named
express.privatenet.json but the user can override this name if they wish via the
--output option.

> Note, express.privatenet.json isn't a great default file name. Any suggestions
> for a better default will be strongly considered.

Because neo-express is exclusively designed for developer scenarios, private keys
for consensus node and standard account wallets are stored **in the clear**. The
user is reminded not to use these accounts on MainNet whenever a new blockchain
instance or standard wallet is created.

By default, a single-node blockchain is created by default, but the user can
create a four or seven node blockchain via the --count option. A single node
blockchain uses less resources and support developer scenarios such as checkpoint
and debugging that are not possible with a multi-node blockchain. However, a
multi-node blockchain provides an environment that more closely mirrors the
production blockchain environment.

### neo-express run

Once a blockchain has been created, the developer can start the blockchain via
the run command. The run command starts a single node of the block chain - the
developer must pass the zero-based node index as the first argument to the run
command. For a single node blockchain, the developer would call `neo-express run 0`.
For a four node blockchain, the developer would need four separate terminal
windows, each running a different node index from 0 to 3.

While blocks in the neo-express blockchain are minted at the same rate as MainNet
by default, the developer can choose to run the blockchain as fast or slow as
they wish via the --seconds-per-block argument. This argument takes an integer
value, indicating how often (in seconds) a new block is created. For developer
purposes, it is often desirable to run the blockchain as fast as possible - one
second per block. This allows the accounts on the blockchain to earn gas quickly
and improves the wait time on blockchain operations such as asset transfer or
smart contract invocation. In a multi-node chain, all nodes must be running at
the same speed.

### neo-express export

neo-express does not use the same wallet, config or protocol files as neo-cli or
neo-gui. To enables those tools to connect to a neo-express blockchain instance,
the developer can invoke the export command. This command saves the consensus
node wallets in standard NEP-6 format and generates config.json and protocol.json
files that neo-cli or neo-gui can use. The NEP-6 wallet format encrypts the
private key, so the developer has to specify a password when exporting a blockchain.
However, since the private key is still stored in plain-text in the blockchain
information file, developers are still strongly advised not to use theses accounts
on MainNet or any other production blockchain environment.

## Wallet Management

Developers can create any number of standard wallets for use with a neo-express
blockchain instance. Like consensus node wallets, the private keys are stored in
the clear so that developers don't have to manage passwords. Wallet information
is also stored in the same file with the rest of the blockchain information. This
allows developers to use easy-to-remember nicknames for wallet accounts like "mywallet"
instead of Base58 encoded hashes like "AU9cXDyjnzbgUPG9ycwemZnYDsTuZkUxq3".

Wallets can be listed, deleted and exported. Exporting a standard wallet saves it
in a NEP-6 compatible format as described in the neo-express export section above.

Wallets can be used for asset transfer and smart contract operations, described
in detail below.

## Asset management

Developers can transfer NEO, GAS and NEP-5 tokens among accounts using the transfer
command. THe transfer command takes four parameters - the asset being transferred,
the amount being transferred, the sender and the receiver accounts. As per the
wallet management section above, the sending and receiving wallet accounts are
specified by friendly name rather than base58 encoded address. Note, the nickname
"genesis" is reserved for use by the multi-sig contract that controls the genesis
tokens created by any new NEO blockchain instance.

Developers can also inspect account info for specific wallets and view/claim
their GAS. For NEO 2, they can get a list of all the UTXO transactions their account
has participated in.

## Contract Management

Like consensus node and wallet information, smart contract information is stored
in the blockchain instance JSON file. Compiled smart contract are imported via the
`neo-express contract import` command. This command pulls the binary AVM/NVM file,
the contents of the abi.json file (which is used for contract parameter parsing during
invocation) as well as a custom metadata.json file that includes all the metadata
needed for deployment of smart contracts in NEO 2.

> Note, the metadata.json file is generated by a custom fork of the neon compiler.
> This will only be needed for NEO 2 blockchains. NEO 3 does away with most of this
> metadata and will be generating a standard manifest file as part of the compile
> process for the metadata that is needed.

Contracts that have been imported can be deployed. Contracts that have been deployed
can be invoked. For deployment, the user must specify a wallet (by nickname) that
will pay the contract deployment GAS cost.

## Checkpoints

As a developer tool, neo-express needs to support repeatability for test and debugging
purposes. neo-express enables the developer to checkpoint single-node blockchain
instances in a known state. This checkpoint can be shared with other developers
or checked into source control.

> Note, multi-node neo-express blockchains do not support checkpoint features.

In order to support checkpoints, neo-express does not use the leveldb based data
store that neo-cli and neo-gui use. This implies that while neo-express can export
wallet and blockchain information so that a neo-cli or neo-gui instance can interact
with the neo-express blockchain, the blockchain storage files are not compatible
across tools.

neo-express uses RocksDB, an evolution of the original leveldb project, but adding
additional features like checkpoint. neo-express uses an existing project RocksDbSharp
project, which has not been vetted for security purposes.

> Note, at this time the blockchain must be stopped in order for a checkpoint to
> be created. The underlying RocksDB datastore does support live checkpoints, so
> it would be possible to add support for checkpointing a blockchain instance while
> it is running.

Checkpoints can be restored, imported or run.

> Checkpoint import has not been implemented yet.

When a checkpoint is restored, the current state of the blockchain is discarded
and replaced with the contents of the checkpoint. Unless there are other
checkpoints that were taken after the restored checkpoint, this operation is
irreversible.

When a checkpoint is run, the specified checkpoint is opened in read-only mode.
Any changes to the blockchain are stored in memory. These changes are discarded
when the blockchain shuts down. There is no way to save the changes of a checkpoint
that was run in this fashion. Live checkpoints - when implemented - will not
be supported when running an existing checkpoint.

Checkpoint run vs restore are intended for different usage scenarios. Checkpoint
restore is for experimentation - saving state before trying out things that may
or may not work, providing a way to go back to an earlier known state if the
experiment goes wrong. Checkpoint run is for testing scenarios - where you want to
run a set of tests against a known state, but don't care about saving the resulting
blockchain once the tests have been validated.

## Assorted Notes

### Remote RPC API

Most of the operations supported by neo-express are implemented as a custom RPC API.
This API is implemented as an RPC plugin that is hard coded into the neo-express
application. If there was interest, it would be possible to refactor the plugin
so that it would be in a seperate DLL and usable by neo-cli.

### Signing

All operations that involve signing - including transfers, GAS claims, contract
deployments and contract invocation - send the data to be signed back to the RPC
client. This way, the blockchain instance doesn't need to manage client wallets.
Even genesis transfer, which requires multiple signatures on multi-node block chains,
send the to-be-signed data back to the client for signing. Of course, in a
neo-express blockchain, the private keys for all wallets are stored in the clear
in a single JSON file. However, the basic client signing model could be used for
other scenarios involving production blockchains.

## Future Features

Visual Studio Code integration is the top feature still to be implemented for
neo-express. This includes a few things (so far):

- Supporting JSON-RPC style control over standard I/O. VSCode uses a similar
  approach for [debug adapters](https://microsoft.github.io/debug-adapter-protocol/)
  and [language servers](https://microsoft.github.io/language-server-protocol/).
- visual blockchain explorer, similar to neoscan or neotracker
- menu commands for common neo express operations, particularly contract deployment
- user friendly interface for specifying parameters for contract invocation
