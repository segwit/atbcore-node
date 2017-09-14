# Setting up Development Environment

## Install Node.js

Install Node.js by your favorite method, or use Node Version Manager by following directions at https://github.com/creationix/nvm

```bash
nvm install v4
```

## Fork and Download Repositories

To develop atbcore-node:

```bash
cd ~
git clone git@github.com:<yourusername>/atbcore-node.git
git clone git@github.com:<yourusername>/atbcore-lib.git
```

To develop ATBcoin or to compile from source:

```bash
git clone git@github.com:<yourusername>/bitcoin.git
git fetch origin <branchname>:<branchname>
git checkout <branchname>
```
**Note**: See ATBcoin documentation for building ATBcoin on your platform.


## Install Development Dependencies

For Ubuntu:
```bash
sudo apt-get install libzmq3-dev
sudo apt-get install build-essential
```
**Note**: Make sure that libzmq-dev is not installed, it should be removed when installing libzmq3-dev.


For Mac OS X:
```bash
brew install zeromq
```

## Install and Symlink

```bash
cd atbcore-lib
npm install
cd ../atbcore-node
npm install
```
**Note**: If you get a message about not being able to download ATBcoin distribution, you'll need to compile atbcoind from source, and setup your configuration to use that version.


We now will setup symlinks in `atbcore-node` *(repeat this for any other modules you're planning on developing)*:
```bash
cd node_modules
rm -rf atbcore-lib
ln -s ~/atbcore-lib
rm -rf atbcoind-rpc
ln -s ~/atbcoind-rpc
```

And if you're compiling or developing ATBcoin:
```bash
cd ../bin
ln -sf ~/atbcoind/src/atbcoind
```

## Run Tests

If you do not already have mocha installed:
```bash
npm install mocha -g
```

To run all test suites:
```bash
cd atbcore-node
npm run regtest
npm run test
```

To run a specific unit test in watch mode:
```bash
mocha -w -R spec test/services/atbcoind.unit.js
```

To run a specific regtest:
```bash
mocha -R spec regtest/atbcoind.js
```

## Running a Development Node

To test running the node, you can setup a configuration that will specify development versions of all of the services:

```bash
cd ~
mkdir devnode
cd devnode
mkdir node_modules
touch atbcore-node.json
touch package.json
```

Edit `atbcore-node.json` with something similar to:
```json
{
  "network": "livenet",
  "port": 3001,
  "services": [
    "atbcoind",
    "web",
    "insight-api",
    "insight-ui",
    "<additional_service>"
  ],
  "servicesConfig": {
    "atbcoind": {
      "spawn": {
        "datadir": "/home/<youruser>/.atbcoin",
        "exec": "/home/<youruser>/atbcoin/src/atbcoind"
      }
    }
  }
}
```

**Note**: To install services [insight-api](https://github.com/bitpay/insight-api) and [insight-ui](https://github.com/bitpay/insight-ui) you'll need to clone the repositories locally.

Setup symlinks for all of the services and dependencies:

```bash
cd node_modules
ln -s ~/atbcore-lib
ln -s ~/atbcore-node
ln -s ~/insight-api
ln -s ~/insight-ui
```

Make sure that the `<datadir>/atbcoin.conf` has the necessary settings, for example:
```
server=1
whitelist=127.0.0.1
txindex=1
addressindex=1
timestampindex=1
spentindex=1
zmqpubrawtx=tcp://127.0.0.1:28332
zmqpubhashblock=tcp://127.0.0.1:28332
rpcallowip=127.0.0.1
rpcuser=atbcoin
rpcpassword=atbcoinpassword
```

From within the `devnode` directory with the configuration file, start the node:
```bash
../atbcore-node/bin/atbcore-node start
```