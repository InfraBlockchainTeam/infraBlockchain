# Install the Contract Dev Toolkit

## Homebrew (Mac OS X)

{% hint style="info" %}
brew install is not working now
{% endhint %}

### Install

```
brew tap infrablockchain/infrablockchain.cdt
brew install infrablockchain.cdt
```

### Uninstall

```
brew remove infrablockchain.cdt
```

## Ubuntu (Debian)

{% hint style="info" %}
Binary is not ready
{% endhint %}

### Install

```
wget https://github.com/EOSIO/eosio.cdt/releases/download/v1.6.3/eosio.cdt_1.6.3-1-ubuntu-18.04_amd64.deb

sudo apt install ./eosio.cdt_1.6.3-1_amd64.deb
```

### Uninstall

```
sudo apt remove eosio.cdt
```

## CentOS/Redhat (RPM)

{% hint style="info" %}
Binary is not ready
{% endhint %}

### Install

```
wget https://github.com/EOSIO/eosio.cdt/releases/download/v1.6.3/eosio.cdt-1.6.3-1.el7.x86_64.rpm

sudo yum install ./eosio.cdt-1.6.3-1.el7.x86_64.rpm
```

### Uninstall

```
$ sudo yum remove eosio.cdt
```

## Install from Source

The location where `infrablockchain.cdt` is cloned is not that important because you will be installing `infrablockchain.cdt` as a local binary in later steps. For now, you can clone `infrablockchain.cdt` to your "contracts" directory previously created, or really anywhere else on your local system you see fit.

```
cd CONTRACTS_DIR
```

### Download

Clone `infrablockchain.cdt` repository.

```
git clone --recursive https://github.com/InfraBlockchain/infrablockchain.cdt
cd infrablockchain.cdt
```

In case you are using a virtual machine. It should be configured with at least 2 CPUs (does not have to be two physical ones) and 8G of memory to avoid compilation errors

### Build

```
./build.sh
```

#### Install

```
sudo ./install.sh
```

The above command needs to be ran with `sudo` because `infrablockchain.cdt`'s various binaries will be installed locally. You will be asked for your computer's account password.

Installing `infrablockchain.cdt` will make the compiled binary global so it can be accessable anywhere. For this tutorial, **it is strongly suggested that you do not skip the install step for Infrablockchain.cdt**, failing to install will make it more difficult to follow this and other tutorials, and make usage in general more difficult.

## Troubleshooting

WIP

### What's Next?

* [Create Development Wallet](create-development-wallet.md): Steps to create a new development wallet used to store public-private key pair.
