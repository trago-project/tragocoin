![Tragocoin Logo](https://github.com/trago-project/tragocoin/raw/master/logo.png)

# Tragocoin Core staging tree 0.10.0.1"


| [Website](https://www.tragocoin.com) | [Exchange](https://www.tragocoin.com) | [Block Explorer](http://explorer.tragocoin.com/) | [Forum BitcoinTalk](https://bitcointalk.com/) |

What is Tragocoin?
----------------

Tragocoin is an experimental digital currency that enables anonymous, instant
payments to anyone, anywhere in the world. Tragocoin uses peer-to-peer technology
to operate with no central authority: managing transactions and issuing money
are carried out collectively by the network. Tragocoin Core is the name of the open
source software which enables the use of this currency.

For more information, as well as an immediately useable, binary version of
the Tragocoin Core software, see https://www.tragocoin.com


Features
=============

* PoW X16R algorithm.
* Masternode System.
* Governance System.
* Super Block System.
* Mega Block System.
* DarkSend & InstantSend.
* Anonymous & Instant Transaction.


## Coin Specifications

| Specification | Value |
|:-----------|:-----------|
| Name | `Tragocoin` |
| Currency | `TRAGO` |
| Total Supply | `25,000,000` |
| Block Size | `4MB` |
| Block Time | `2.5 Minutes` |
| PoW Normal Reward | `5 TRAGO` |
| PoW Mega Reward | `200 TRAGO` |
| Masternode Collateral | `20,000 TRAGO` |
| Masternode Reward | `50% Of Block Reward` |
| Masternode Start | `Friday, July 12, 2019 3:00:00 AM` |
| Port | `9420` |
| RPC Port | `9421` |
| Masternode Fixed Port | `9420` |


## Block Rewards 

| Days | PoW Reward | Miner Reward | MN Reward |
|:-----------|:-----------|:-----------|:-----------|
| 1 | `5 TRAGO` | `5 TRAGO` | `None` |
| 2 | `20 TRAGO` | `20 TRAGO` | `None` |
| 3 - 7 | `100 TRAGO` | `100 TRAGO` | `None` |
| 8 - 15 | `100 TRAGO` | `50 TRAGO` | `50 TRAGO` |
| 16 | `75 TRAGO` | `37.5 TRAGO` | `37.5 TRAGO` |
| 17 | `50 TRAGO` | `25 TRAGO` | `25 TRAGO` |
| 18 | `25 TRAGO` | `12.5 TRAGO` | `12.5 TRAGO` |
| 19 | `10 TRAGO` | `5 TRAGO` | `5 TRAGO` |
| 20 ~ | `5 TRAGO` | `2.5 TRAGO` | `2.5 TRAGO` |



| Monthly Mega Block | PoW Reward | Miner Reward | MN Reward |
|:-----------|:-----------|:-----------|:-----------|
| Year 1 | `200 TRAGO` | `100 TRAGO` | `100 TRAGO` |
| Year 2 | `100 TRAGO` | `60 TRAGO` | `40 TRAGO` |
| Year 3 ~ | `None` | `None` | `None` |



Build Tragocoin Wallet
----------

### Building for 64-bit Windows

The first step is to install the mingw-w64 cross-compilation tool chain. Due to different Ubuntu packages for each distribution and problems with the Xenial packages the steps for each are different.

Common steps to install mingw32 cross compiler tool chain:

    sudo apt install g++-mingw-w64-x86-64
    
Ubuntu Xenial 16.04 and Windows Subsystem for Linux

    sudo apt install software-properties-common
    sudo add-apt-repository "deb http://archive.ubuntu.com/ubuntu zesty universe"
    sudo apt update
    sudo apt upgrade
    sudo update-alternatives --config x86_64-w64-mingw32-g++ # Set the default mingw32 g++ compiler option to posix.
    
Once the tool chain is installed the build steps are common:

Note that for WSL the tragocoin Core source path MUST be somewhere in the default mount file system, for example /usr/src/tragocoin, AND not under /mnt/d/. If this is not the case the dependency autoconf scripts will fail. This means you cannot use a directory that located directly on the host Windows file system to perform the build.

The next three steps are an example of how to acquire the source in an appropriate way.

    cd /usr/src
    sudo git clone https://github.com/trago-project/tragocoin.git
    sudo chmod -R a+rw tragocoin
    
Once the source code is ready the build steps are below.

    PATH=$(echo "$PATH" | sed -e 's/:\/mnt.*//g') # strip out problematic Windows %PATH% imported var
    cd depends
    make HOST=x86_64-w64-mingw32 -j4
    cd ..
    ./autogen.sh # not required when building from tarball
    CONFIG_SITE=$PWD/depends/x86_64-w64-mingw32/share/config.site 
    ./configure --prefix=`pwd`/depends/x86_64-w64-mingw32
    make

### Build on Ubuntu

    sudo apt-get install build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils git cmake libboost-all-dev
    sudo apt-get install software-properties-common
    sudo add-apt-repository ppa:bitcoin/bitcoin
    sudo apt-get update
    sudo apt-get install libdb4.8-dev libdb4.8++-dev

    # If you want to build the Qt GUI:
    sudo apt-get install libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev protobuf-compiler

    git clone https://github.com/trago-project/tragocoin --recursive
    
    cd tragocoin

    # Note autogen will prompt to install some more dependencies if needed
    ./autogen.sh
    ./configure
    make -j4

### Build on OSX

The commands in this guide should be executed in a Terminal application.
The built-in one is located in `/Applications/Utilities/Terminal.app`.

#### Preparation

Install the OS X command line tools:

`xcode-select --install`

When the popup appears, click `Install`.

Then install [Homebrew](https://brew.sh).

#### Dependencies

    brew install cmake automake berkeley-db4 libtool boost --c++11 --without-single --without-static miniupnpc openssl pkg-config protobuf qt5 libevent imagemagick --with-librsvg

NOTE: Building with Qt4 is still supported, however, could result in a broken UI. Building with Qt5 is recommended.

#### Build Tragocoin Core

1. Clone the tragocoin source code and cd into `tragocoin`

        git clone --recursive https://github.com/trago-project/tragocoin.git
        cd tragocoin

2.  Build Tragocoin Core:

    Configure and build the headless tragocoin binaries as well as the GUI (if Qt is found).

    You can disable the GUI build by passing `--without-gui` to configure.

        ./autogen.sh
        ./configure
        make


### Run

Then you can either run the command-line daemon using `src/tragocoind` and `src/tragocoin-cli`, or you can run the Qt GUI using `src/qt/tragocoin-qt`

For in-depth description of Sparknet and how to use Tragocoin for interacting with contracts, please see [sparknet-guide](doc/sparknet-guide.md).


### Mining

Create an TRAGO Wallet. Setup your tragocoin.conf file. download miner software https://www.tragocoin.com 

Example commandline for cpuminer is:

./cpuminer -a x16r -o http://127.0.0.1:37001/ -u rpcUserXX -p rpcPasswprdXX --coinbase-add=TmmDpEvmgrxxxxxxxxxxxxxxxxxxxxxxx --no-getwork --debug

Coinbase address is the wallet address you would like the reward to goto. Debug is always helpful.


### Building a masternode

Setting up a masternode requires a basic understanding of Linux and blockchain technology, as well as an ability to follow instructions closely. It also requires regular maintenance and careful security. Full guide instructions setup : https://www.tragocoin.com/page/setup


Development Process
-------------------

The `master` branch is regularly built and tested, but is not guaranteed to be
completely stable. [Tags](https://github.com/trago-project/tragocoin/tags) are created
regularly to indicate new official, stable release versions of Tragocoin.

The contribution workflow is described in [CONTRIBUTING.md](CONTRIBUTING.md).


Testing
-------

Testing and code review is the bottleneck for development; we get more pull
requests than we can review and test on short notice. Please be patient and help out by testing
other people's pull requests, and remember this is a security-critical project where any mistake might cost people
lots of money.

### Automated Testing

Developers are strongly encouraged to write [unit tests](src/test/README.md) for new code, and to
submit new unit tests for old code. Unit tests can be compiled and run
(assuming they weren't disabled in configure) with: `make check`. Further details on running
and extending unit tests can be found in [/src/test/README.md](/src/test/README.md).

There are also [regression and integration tests](/qa) of the RPC interface, written
in Python, that are run automatically on the build server.
These tests can be run (if the [test dependencies](/qa) are installed) with: `qa/pull-tester/rpc-tests.py`

### Manual Quality Assurance (QA) Testing

Changes should be tested by somebody other than the developer who wrote the
code. This is especially important for large or high-risk changes. It is useful
to add a test plan to the pull request description if testing the changes is
not straightforward.

## License

MIT License

Copyright (c) 2019 Tragocoin

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

=======
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
