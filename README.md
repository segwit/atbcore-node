ATBcore Node
============

A ATBcoin full node for building applications and services with Node.js. A node is extensible and can be configured to run additional services. At the minimum a node has an interface to [ATBcoin Core with additional indexing](https://github.com/segwit/atbcoin) for more advanced address queries. Additional services can be enabled to make a node more useful such as exposing new APIs, running a block explorer and wallet service.

## Install

```bash
npm install -g atbcore-node
atbcore-node start
```

Note: For your convenience, we distribute atbcoind binaries for x86_64 Linux and x86_64 Mac OS X. Upon npm install, the binaries for your platform will be downloaded. For more detailed installation instructions, or if you want to compile the project yourself, then please see the ATBcore branch of [ATBcoin Core with additional indexing](https://github.com/segwit/atbcoin).

## Configuration

ATBcore includes a Command Line Interface (CLI) for managing, configuring and interfacing with your Atbcore Node.

```bash
atbcore-node create -d <atbcoin-data-dir> mynode
cd mynode
atbcore-node install <service>
atbcore-node install https://github.com/yourname/helloworld
```

This will create a directory with configuration files for your node and install the necessary dependencies. For more information about (and developing) services, please see the [Service Documentation](docs/services.md).

## Add-on Services

There are several add-on services available to extend the functionality of ATBcore:

- [ATB Insight API](https://github.com/segwit/atb-insight-api)
- [ATB Insight UI](https://github.com/segwit/atb-insight-ui)

## Documentation

- [Upgrade Notes](docs/upgrade.md)
- [Services](docs/services.md)
  - [ATBcoind](docs/services/atbcoind.md) - Interface to ATBcoin Core
  - [Web](docs/services/web.md) - Creates an express application over which services can expose their web/API content
- [Development Environment](docs/development.md) - Guide for setting up a development environment
- [Node](docs/node.md) - Details on the node constructor
- [Bus](docs/bus.md) - Overview of the event bus constructor
- [Release Process](docs/release.md) - Information about verifying a release and the release process.

## License

Code released under the MIT license