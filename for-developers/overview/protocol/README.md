---
description: >-
  Please note: All the details described below which is applicable to EOSIO,
  applies to InfraBlockchain.
---

# Protocol

## Core <a href="#core" id="core"></a>

`EOSIO Core` provides the basic building blocks for the `system` layer and because they are not implemented as smart contracts they do not provide the same level of flexibility. Nevertheless, the `core` implementation is also open source and thus it can be modified as well to suit custom business requirements.The core protocols are:

1. ​[Consensus Protocol](consensus-protocol.md)
2. ​[Transactions Protocol](transactions-protocol.md)
3. [Network Peer Protocol](network-peer-protocol.md)​
4. [Accounts & Permissions](accounts-and-permissions.md)

## System <a href="#system" id="system"></a>

The EOSIO blockchain platform is unique in that the features and characteristics of the blockchain built on it are flexible, that is, they can be changed, or be modified completely to suit each business case requirement. Core blockchain features such as consensus, fee schedules, account creation and modification, token economics, block producer registration, voting, multi-sig, etc., are implemented inside smart contracts which are deployed on the blockchain built on the EOSIO platform. These smart contracts are referred to as `system contracts` and the layer as the `EOSIO system` layer, or simply `system` layer.&#x20;

1. ​[infra.system](../../developer-guides-infrablockchain-native/infrablockchain-system-contracts/infra.system/)
2. [sys.tokenabi](../../developer-guides-infrablockchain-native/infrablockchain-system-contracts/sys.tokenabi/)​
