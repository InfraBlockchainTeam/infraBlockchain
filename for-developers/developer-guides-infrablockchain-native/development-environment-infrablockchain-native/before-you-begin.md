# Before You Begin

## Step 1: Install binaries

To get started as quickly as possible we recommend using pre-built binaries. Building from source is a more advanced option but will set you back an hour or more and you may encounter build errors.

You can find how to build InfraBlockchain from source [here](https://github.com/InfraBlockchain/infrablockchain).

The below commands will download binaries for respective operating systems.

### Mac OS X Brew Install:

{% hint style="info" %}
brew Install is not working now
{% endhint %}

```
brew tap infrablockchain/infrablockchain
brew install infrablockchain
```

If you don't have Brew installed, follow the installation instructions on the [official Brew website](https://brew.sh/).

### Ubuntu 18.04 Debian Package Install:

```
wget https://github.com/InfraBlockchain/infrablockchain/releases/download/v2.3.0-rc1/infrablockchain-2.3.0-rc1-amd64.deb
sudo apt install ./infrablockchain-2.3.0-rc1-amd64.deb
```

### Ubuntu 16.04 Debian Package Install:

```
wget https://github.com/InfraBlockchain/infrablockchain/releases/download/v2.3.0-rc1/infrablockchain-2.3.0-rc1-amd64.deb
sudo apt install ./infrablockchain-2.3.0-rc1-amd64.deb
```

### CentOS RPM Package Install:

```
wget https://github.com/InfraBlockchain/infrablockchain/releases/download/v2.3.0-rc1/infrablockchain-2.3.0-rc1.x86_64.rpm
sudo yum install ./infrablockchain-2.3.0-rc1.x86_64.rpm
```

If you have previous versions of Infrablockchain installed on your system, please uninstall before proceeding.

## Step 2: Setup a development directory, stick to it.

You're going to need to pick a directory to work from, it's suggested to create a `contracts` directory somewhere on your local drive.

```
mkdir contracts
cd contracts
```

## What's Next?

* [Install the CDT](install-the-contract-dev-toolkit.md): Steps to install the InfraBlockchain Contract Development Toolkit (CDT) on your system.
