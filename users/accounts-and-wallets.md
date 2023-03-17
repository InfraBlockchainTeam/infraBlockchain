# Accounts and Wallets

## Account On InfraBlockchain

All accounts on InfraBlockchain are identified by a twelve character (human-readable) name. This account name represents an uint64\_t (unsigned 64-bit integer) identifying the account. This integer is not the account’s public key, neither is it directly related to a specific key-pair. This account name is controlled by one or more key-pairs (which can be updated).

If there is a private key which controls the account _ACCOUNT\_NAME_, that private key can be updated to a new key. Multiple key-pairs can control that specific account, each with specific permissions. By default, the key permissions are “active” and “owner”.

An active key is allowed to take any action (token transfers, pushing actions to applications, etc). The active permission is allowed to update and change its key, but it cannot change the owner’s key.

The owner account has the exclusive function to change its own key, and always the ability to change the active key. This adds an extra layer of security to the system. In the event that an active key has been compromised, the owner key can update the active key.

More specific actions and permissions can be set-up, like multi-signature permissions attached to specific actions (as defined by the smart contract).

## What is a Wallet?

A blockchain wallet (e-wallet, crypto wallet or signer) is a tool that you use to interact with a blockchain network. It is a digital wallet that allows users to store and manage their digital private key. A blockchain wallet allows to take any action and push transaction to blockchain network.

A wallet can either be a device or application that stores a collection of cryptographic keys and can be used to send, receive, and track ownership of cryptocurrencies. Wallets can take many forms. A wallet might be a directory or file in your computer's file system, a piece of paper, or a specialized device called a _hardware wallet_. There are also various smartphone apps and computer programs that provide a user-friendly way to create and manage wallets.

When interacting with the InfraBlockchain, your choice of wallet software for safely storing and utilizing your tokens is one of the most critical decisions that you can make. Important factors include security, usability, and integrations for dApps and trading. Your wallet is your doorway into the InfraBlockchain network.

Once you have created your InfraBlockchain account, and linked it with your wallet provider, then you are ready to start interacting with the InfraBlockchain network.

## **Desktop Wallets**

The desktop version enables users to store their wallet directly on their computer.

### InfraBlockchain Native

* WIP

### InfraBlockchain EVM

* WIP

## **Mobile Wallets**

* WIP

## Command-Line **Wallet**

* infra-cli: developed by [InfraBlockchain](https://github.com/InfraBlockchain)
