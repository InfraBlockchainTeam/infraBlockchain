# Technical Features

## WebAssembly C++ Compilation

InfraBlockchain uses C++ as the smart contract programming language. If you are a C++ developer, you do not need to learn a new programming language to understand Smart Contract APIs and how InfraBlockchain supports smart contract development through C++ classes and structures. With your existing C++ programming capabilities, you can onboard InfraBlockchain development faster and be able to program InfraBlockchain contracts using specific EOSIO canonical C++ code constructs and Smart Contract APIs in no time.

On top of the InfraBlockchain core layer, a WebAssembly (Wasm) virtual machine, `EOS VM`, executes smart contract code, and it is designed from the ground up for the high demands of blockchain applications which require far more from a WebAssembly engine than those designed for web browsers or standards development.&#x20;

The design choice of using Wasm enables InfraBlockchain to reuse optimized and battle-tested compilers and toolchains which are being maintained and improved by a broader community. In addition, adopting Wasm standard also makes it easier for compiler developers to port other programming languages onto the InfraBlockchain platform.

## High Throughput, Faster Confirmations and Lower Latency

InfraBlockchain is designed with high transactions throughput in mind and each new version is achieving significant improvements.

The consensus mechanism of Delegated Proof of Stake (DPoS) achieves high transaction throughputs because DPOS does not need to wait for all the nodes to complete a transaction to achieve finality. This behavior results in faster confirmations and lower latency.

The `EOS-VM` mentioned earlier, and all its blockchain-dedicated features and improvements add significant contribution to the overall performance of the InfraBlockchain network and any EOSIO-based blockchain.

## Programmable Economics and Governance

The resource allocation and governance mechanism for the InfraBlockchain network are programmable through smart contracts. You can modify the system smart contracts to customize the resource allocation model and governance rules for the InfraBlockchain network The on-chain governance mechanism can be modified using system smart contracts, as the core layer code does not always have to be updated for the changes to take place.

## Comprehensive Permission Schema

The InfraBlockchain platform has a comprehensive permission system for creating custom permission schemata for various use cases. For example, you can create a custom permission and use it to protect a specific feature of a smart contract. You can also split the authority required to modify a smart contract across multiple accounts with different levels of authority. This comprehensive permission system allows you to build a permissioned application on top of a flexible infrastructure.

## Upgradability

Applications deployed on InfraBlockchain are upgradeable. This means you can deploy code fix, add features, and change the application’s logic, as long as sufficient authority is provided. As a developer, you can iterate your application without the risk of being locked-in to a software bug permanently. It is also possible, however, to deploy smart contracts that cannot be modified on the InfraBlockchain network. These decisions are at the discretion of developers rather than restricted by the protocol.

## Efficient energy consumption

With `PoT` as the consensus mechanism, InfraBlockchain consumes much less energy to validate transactions and secure a blockchain compared to other consensus algorithms.
