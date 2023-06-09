# Create Test Accounts

## NOTE - You can get accounts and testnet system token at the testnet faucet, the steps below are only for a local testnet

## What is an account?

An account is a collection of authorizations, stored on the blockchain, and used to identify a sender/recipient. It has a flexible authorization structure that enables it to be owned either by an individual or group of individuals depending on **how** permissions have been configured. An account is required to send or receive a valid transaction to the blockchain

This tutorial series uses two "user" accounts, `bob` and `alice`, as well as the default `eosio` account for configuration. Additionally accounts are made for various contracts throughout this tutorial series.

## Step 1: Create Test Accounts

**Public Key Persistence** In section **1.4 Create Development Wallet**, you created a development key pair and pasted the public key in the **Development Public Key** field for the value to persist throughout the tutorial.

In the following steps, if you see `YOUR_PUBLIC_KEY` instead of the public key value, you can either go back to section **1.4 Create Development Wallet** and persist the value or replace `YOUR_PUBLIC_KEY` with the public key value manually.

Throughout these tutorials the accounts `bob` and `alice` are used. Create two accounts using `infra-cli create account`

```
infra-cli create account eosio bob YOUR_PUBLIC_KEY
infra-cli create account eosio alice YOUR_PUBLIC_KEY
```

You should then see a confirmation message similar to the following for each command that confirms that the transaction has been broadcast.

```
executed transaction: 40c605006de...  200 bytes  153 us
#         eosio <= eosio::newaccount            {"creator":"eosio","name":"alice","owner":{"threshold":1,"keys":[{"key":"EOS5rti4LTL53xptjgQBXv9HxyU...
warning: transaction executed locally, but may not be confirmed by the network yet    ]
```

## Step 2: Public Key

Note in `infra-cli` command a public key is associated with account `alice`. Each InfraBlockchain account is associated with a public key.

Be aware that the account name is the only identifier for ownership. You can change the public key but it would not change the ownership of your InfraBlockchain account.

Check which public key is associated with `alice` using `infra-cli get account`

```
infra-cli get account alice
```

You should see a message similar to the following:

```
permissions:
     owner     1:    1 EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV
        active     1:    1 EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV
memory:
     quota:       unlimited  used:      3.758 KiB

net bandwidth:
     used:               unlimited
     available:          unlimited
     limit:              unlimited

cpu bandwidth:
     used:               unlimited
     available:          unlimited
     limit:              unlimited
```

Notice that actually `alice` has both `owner` and `active` public keys. InfraBlockchain has a unique authorization structure that has added security for your account. You can minimize the exposure of your account by keeping the owner key cold, while using the key associated with your `active` permission. This way, if your `active` key were ever compromised, you could regain control over your account with your `owner` key.

In term of authorization, if you have a `owner` permission you can change the private key of `active` permission. But you cannot do so other way around.&#x20;

{% hint style="info" %}
In this tutorial we are using the same public key for both `owner` and `active` for simplicity. In production network, two different keys are strongly recommended
{% endhint %}

## Troubleshooting

If you get an error while creating the account, make sure your wallet is unlocked

```
infra-cli wallet list
```

You should see an asterisk (`*`) next to the wallet name, as seen below.

```
Wallets:
[
  "default *"
]
```

## What's Next?

* [Hello World](../smart-contract-development/hello-world-contract.md): The Hello World of Infrablockchain! Learn how to set up your environment and deploy your first smart contract.
