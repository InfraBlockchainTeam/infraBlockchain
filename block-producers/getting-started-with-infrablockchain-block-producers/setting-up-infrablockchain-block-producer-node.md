# Setting up InfraBlockchain Block Producer node

## Installation Methods

* InfraBlockchain currently supports the following operating systems:
  * Amazon Linux 2
  * CentOS 7
  * Ubuntu 16.04
  * Ubuntu 18.04
  * MacOS 10.14 (Mojave)

> NOTE: If you are new to InfraBlockchain, it is recommended that you install the InfraBlockchain Prebuilt Binaries. If you are an advanced developer, a block producer, or no binaries are available for your platform, you may need to Build InfraBlockchain from source depending on your OS.

### Ubuntu package method

```
$ wget https://github.com/InfraBlockchain/infrablockchain/releases/download/v2.3.0-rc1/infrablockchain-2.3.0-rc1-amd64.deb
$ sudo apt install ./infrablockchain-2.3.0-rc1-amd64.deb
```

### Compile source code method

1.  Clone the `InfraBlockchain/infrablockchain` repository from Github like this:

    ```
    $ git clone https://github.com/InfraBlockchain/infrablockchain.git --recursive` [NOT NEEDED, if already cloned]
    ```

> NOTE: The step-1 is not needed, if the repository is already cloned. Directly, start from step-2.

1.  Go to the `infrablockchain` folder&#x20;

    ```
    $ cd infrablockchain
    ```
2.  pull the repository with required released version&#x20;

    ```
    $ git pull https://github.com/InfraBlockchain/infrablockchain.git v2.3.0-rc1
    ```
3.  update the submodules

    ```
    $ git submodule update --init --recursive
    ```
4.  Go to required version

    ```
    $ git checkout tags/v2.3.0-rc1
    ```

## Run Infra-node

`infra-node` generally runs in 2 modes:

### A. Producing/Active mode

`Producing Validator Nodes` are configured for block production. They connect to the peer-to-peer (p2p) network and actively produce new blocks. Loose transactions are also validated and relayed. On mainnet, Producing Validator Nodes only produce blocks if their assigned block producer is part of an active schedule.

> NOTE: System contracts required - These instructions assume you want to launch a producing validator node on a network with system contracts loaded. These instructions will not work on a default development node using native functionality, or one without system contracts loaded.

#### Goal

This section describes how to set up a producing node within the InfraBlockchain network. A producing node, as its name implies, is a node that is configured to produce blocks in an InfraBlockchain based blockchain. This functionality if provided through the producer\_plugin as well as other infra-node Plugins.

**infra-node plugins**

* Plugins extend the core functionality implemented in `infra-node`. Some plugins are mandatory, such as `chain_plugin`, `net_plugin`, and `producer_plugin`, which reflect the modular design of `infra-node`. The other plugins are optional as they provide nice to have features, but non-essential for the nodes operation.
* The list of specific plugins are as follows:
  * `chain_api_plugin`
  * `chain_plugin`
  * `db_size_api_plugin`
  * `history_api_plugin`
  * `history_plugin`
  * `http_client_plugin`
  * `http_plugin`
  * `login_plugin`
  * `net_api_plugin`
  * `net_plugin`
  * `producer_plugin`
  * `state_history_plugin`
  * `trace_api_plugin`
  * `txn_test_gen_plugin`

> Infra-node is modular: Plugins add incremental functionality to `infra-node`. Unlike runtime plugins, infra-node plugins are built at compile-time.

#### Pre-requisites

* Install the [InfraBlockchain software](https://github.com/InfraBlockchain/infrablockchain) before starting this section.
* It is assumed that `infra-node`, `infra-cli`, and `infra-keychain` are accessible through the path. If you built InfraBlockchain using shell scripts, make sure to run the Install Script.
* Know how to pass Infra-node options to enable or disable functionality.

#### Steps

Please follow the steps below to set up a producing node:

1. Local Wallet
2. Register your account as a producing validator
3. Set Producer Name
4. Set the Producer's signature-provider
5. Define a peers list
6. Load the Required Plugins

**1. Local Wallet**

**a. Create InfraBlockchain Wallet locally. Record the password and keep secure.**

```
infra-cli wallet create -n <wallet_name> --to-console
<!-- OR -->
infra-cli wallet create -n <wallet_name> --file <filename_with_extension>
```

**b. Unlock InfraBlockchain Wallet. Paste your wallet password**

```
infra-cli wallet unlock -n <wallet_name> --password <wallet_password>
```

**c. Account creation:**

```
infra-cli -u <api_endpoint> system newaccount --stake-net <net_amount> --stake-cpu <cpu_amount> --buy-ram-kbytes <ram_amount> <existing_account_name> <existing_account_name> <owner-publickey> <active-publickey>
```

**d. Load new account private key into your wallet**

```
infra-cli wallet import -n <wallet_name> <privkey>
```

**2. Register your account as a producing validator**

In order for your account to be eligible as a producing validator, you will need to register the account as a producing validator:

```
<!-- infra-cli -u <api_endpoint> system regproducer <producer_account_name> <producer_signature_public_key> <producer_website> <producer-geo-location> -->
infra-cli -u http://api.main.alohaeos.com system regproducer alohaeosprod EOS87wJkSDXLDVVoJUaBYd4tjg8F8chMWY5nPo8Mb5F919TpbjJvz https://www.alohaeos.com Honolulu
```

> NOTE: separate key pair used only for signing blocks and can not perform any other operation.
>
> If you currently have your active key listed in your `config.ini` for signing blocks — you need to stop it and replace it with a separate Signature key

Just follow this in order to replace the existing active (or insecure key) with separate signature key

* Create new key pair using `infra-cli create key --to-console`
* Replace signature provider record in your `config.ini` with the new key: `signature-provider = EOS-SIGNATURE-PUBLIC-KEY=KEY:SIGNATURE-PRIVATE-KEY`
* Call regproducer command with the new signature key: `infra-cli system regproducer [PRODUCER-NAME] [EOS-SIGNATURE-PUBLIC-KEY] {PRODUCER_URL] [COUNTRY_CODE]`

**4. Set Producer Name**

Set the `validator_name` option in `config.ini` to your account, as follows:

```
# config.ini:

# ID of producer controlled by this node (e.g. inita; may specify multiple times) (eosio::producer_plugin)
producer-name = alohaeosprod
```

**5. Set the Producer's signature-provider**

You will need to set the separate private key for your validator. The public key should have an authority for the validator account defined above.

`signature-provider` is defined with a 3-field tuple:

* `public-key` - A valid EOSIO public key in form of a string.
* `provider-spec` - It's a string formatted like :
* `provider-type` - KEY or Infra-keychain

**Using a Key:**

```
# config.ini:

signature-provider = PUBLIC_SIGNING_KEY=KEY:PRIVATE_SIGNING_KEY

//Example
//signature-provider = EOS51PsUQXRKphEBPBP8iH8ZRGNvyqJ13hbR8yXGSPKEf5TQH27TF=KEY:5KgV1HsxEm3qKYdLaUgpdZvJcAV2AA7zVDJYBL7nVoE4mdcqQR1
```

**6. Define a peers list**

```
# config.ini:

# Default p2p port is 9876
p2p-peer-address = 195.201.82.181:9876
p2p-peer-address = 47.52.71.18:9876
p2p-peer-address = 207.180.220.203:9876
```

For more, visit here for InfraBlockchain-mainnet or InfraBlockchain-testnet

**7. Load the Required Plugins**

In your `config.ini`, confirm the following plugins are loading or append them if necessary.

```
# config.ini:

plugin = eosio::chain_plugin
plugin = eosio::producer_plugin
```

### B. Non-Producing or Standby mode

`Non-Producing Validator Nodes` connect to the peer-to-peer (p2p) network but do not actively produce new blocks; they are useful for acting as proxy nodes, relaying API calls, validating transactions, broadcasting information to other nodes, etc. `Non-Producing Validator Nodes` are also useful for monitoring the blockchain state.

#### Goal

This section describes how to set up a non-producing validator node within the InfraBlockchain network. A non-producing validator node is a node that is not configured to produce blocks, instead it is connected and synchronized with other peers from an InfraBlockchain based blockchain, exposing one or more services publicly or privately by enabling one or more Nodeos Plugins, except the producer\_plugin.

#### Pre-requisites

* Install the [InfraBlockchain software](https://github.com/InfraBlockchain/infrablockchain) before starting this section.
* It is assumed that `infra-node`, `infra-cli`, and `infra-keychain` are accessible through the path. If you built InfraBlockchain using shell scripts, make sure to run the Install Script.
* Know how to pass Infra-cli options to enable or disable functionality.

#### Steps

Please follow the steps below to set up a non-producing node:

1. Set Peers
2. Enable one or more available plugins

**1. Set Peers**

You need to set some peers in your config ini, for example:

```
# config.ini:

# Default p2p port is 9876
p2p-peer-address = 195.201.82.181:9876
p2p-peer-address = 47.52.71.18:9876
p2p-peer-address = 207.180.220.203:9876
```

For more, visit here for Infrablockchain-mainnet or Infrablockchain-testnet

Or you can include the peer in as a boot flag when running `infra-node`, as follows:

```
infra-node ... --p2p-peer-address=106.10.42.238:9876
```

**2. Enable one or more available plugins**

Each available plugin is listed and detailed in the Infra-node Plugins section. When `infra-node` starts, it will expose the functionality provided by the enabled plugins it was started with. For example, if you start `infra-node` with `state_history_plugin` enabled, you will have a non-producing node that offers full blockchain history. If you start `infra-node` with `http_plugin` enabled, you will have a non-producing node which exposes the Telos RPC API. Therefore, you can extend the basic functionality provided by a non-producing node by enabling any number of existing plugins on top of it. Another aspect to consider is that some plugins have dependencies to other plugins. Therefore, you need to satisfy all dependencies for a plugin in order to enable it.

## Configuration Files

### Mainnet

#### genesis.json

```javascript
<NEED TO UPDATE>
```

#### config.ini

```
###### producer plugin options - enable if running producer node
plugin = eosio::producer_plugin
## sig provider keys should match the key on your producer-name
signature-provider = <pubkey>=KEY:<privkey>
producer-name = <your unique Infrablockchain account name>

## additional producer plugin options can be left default
max-transaction-time = 10000
max-irreversible-block-age = -1
abi-serializer-max-time-ms = 2000
enable-stale-production = true
pause-on-startup = false

###### chain plugin options
plugin = eosio::chain_plugin
wasm-runtime = wabt
reversible-blocks-db-size-mb = 340
contracts-console = false
## set chain-state-db-size-mb to equal the size of your RAM
chain-state-db-size-mb = 98304

###### http plugin options
plugin = eosio::http_plugin
http-server-address = 0.0.0.0:1880
access-control-allow-origin = *
access-control-allow-credentials = false
https-client-validate-peers = 1 
verbose-http-errors = true
http-validate-host = 0
## enable if using https
# https-server-address = 0.0.0.0:443
# https-certificate-chain-file

# nodeos general config
p2p-server-address = 0.0.0.0:9876
p2p-listen-endpoint = 0.0.0.0:9876
p2p-max-nodes-per-host = 1
max-clients = 250
connection-cleanup-period = 30
sync-fetch-span = 100
txn-reference-block-lag = 0
allowed-connection = any
agent-name = bensigcoolconfig

###### additional plugins
plugin = eosio::chain_api_plugin
plugin = eosio::history_plugin

###### p2p peer address
<NEED TO UPDATE>
```

### Testnet

#### genesis.json

```javascript
{
  "initial_timestamp": "2022-07-14T00:00:00.000",
  "initial_key": "EOS85C41G7pk4ho5PTBjW7AVjVa2jPiwLfajcysyKtDF6Ld3EY5aN",
  "initial_configuration": {
    "max_block_net_usage": 1048576,
    "target_block_net_usage_pct": 1000,
    "max_transaction_net_usage": 524288,
    "base_per_transaction_net_usage": 12,
    "net_usage_leeway": 500,
    "context_free_discount_net_usage_num": 20,
    "context_free_discount_net_usage_den": 100,
    "max_block_cpu_usage": 200000,
    "target_block_cpu_usage_pct": 1000,
    "max_transaction_cpu_usage": 150000,
    "min_transaction_cpu_usage": 100,
    "max_transaction_lifetime": 3600,
    "deferred_trx_expiration_window": 600,
    "max_transaction_delay": 3888000,
    "max_inline_action_size": 4096,
    "max_inline_action_depth": 4,
    "max_authority_depth": 6
  }
}
```

#### config.ini

```
###### producer plugin options - enable if running producer node
plugin = eosio::producer_plugin
## sig provider keys should match the key on your producer-name
signature-provider = <pubkey>=KEY:<privkey>
producer-name = <your unique Infrablockchain account name>

## additional producer plugin options can be left default
max-transaction-time = 10000
max-irreversible-block-age = -1
abi-serializer-max-time-ms = 2000
enable-stale-production = true
pause-on-startup = false

###### chain plugin options
plugin = eosio::chain_plugin
wasm-runtime = wabt
reversible-blocks-db-size-mb = 340
contracts-console = false
## set chain-state-db-size-mb to equal the size of your RAM
chain-state-db-size-mb = 98304

###### http plugin options
plugin = eosio::http_plugin
http-server-address = 0.0.0.0:1880
access-control-allow-origin = *
access-control-allow-credentials = false
https-client-validate-peers = 1 
verbose-http-errors = true
http-validate-host = 0
## enable if using https
# https-server-address = 0.0.0.0:443
# https-certificate-chain-file

# nodeos general config
p2p-server-address = 0.0.0.0:9876
p2p-listen-endpoint = 0.0.0.0:9876
p2p-max-nodes-per-host = 1
max-clients = 250
connection-cleanup-period = 30
sync-fetch-span = 100
txn-reference-block-lag = 0
allowed-connection = any
agent-name = bensigcoolconfig

###### additional plugins
plugin = eosio::chain_api_plugin
plugin = eosio::history_plugin

###### p2p peer address
<NEED TO UPDATE>
```

## Frequently Asked Questions (FAQs)

#### Q. What is the difference between InfraBlockchain Mainnet and Testnet?

#### A. The differences are as follows:

a. The mainnet of a blockchain launches when the protocol is fully developed and is the network where the project's functionalities, such as transactions with the native tokens, are carried out. Here is where transactions are being broadcasted, verified, and recorded on a distributed ledger technology. Whereas the testnet is a safe, separate network where developers carry out tests in the code without risking the main blockchain. The InfraBlockchain Testnets are a sandbox for testing newly implemented features, finding bugs within the network and developing DApps. a. Testnet is for testing code updates, other functionalities, bug identification, new projects and program development, among many other uses. b. People associate a testnet with the initial developing of a blockchain where all the codes run, and we test everything before the final deployment of the protocol to the mainnet. c. the InfraBlockchain testnets have one prominent advantage over the other testnets: it is a duplicate of the mainnet so it includes all its smart contracts and functionalities in the testnets. Because of this, developers and BPs obtain complete, accurate results when they run their tests, while reducing the work they have to do before running them. e. Testnet is designed to be as close to the code/features of the InfraBlockchain Mainnet, with exception to any new innovations being tested in preparation for deployment on Mainnet.
