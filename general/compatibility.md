---
description: This is a resume of compatibility between the components of the Pantos ecosystem.
---

# Compatibility between versions

## The Pantos ecosystem

The Pantos ecosystem is composed of:
- [Pantos Protocol](XXXX)
  
  The protocol defines the collection of functions exposed in order to get the expected functionality. The signature of this functions can be found [here](XXXXX).

- [Ethereum Contracts](https://github.com/pantos-io/ethereum-contracts)

  A collection of contracts that implement the Pantos protocol. 

- [Service Node](https://github.com/pantos-io/servicenode)
  
  A baseline implementation of a node interacting with the Pantos protocol and the multiple supported blockchains. A service node MUST be able to interact with the latest Pantos Protocol deployed.

- [Validator Node](https://github.com/pantos-io/validatornode)

  A node responsible for validating cross-chain transfers on behalf of the users.

## About the versioning of the Pantos Protocol

The Pantos Protocol is versioned using [semantic versioning](https://semver.org) following the `major.minor.patch` naming convention (e.g. `0.1.0`). However, due to the nature of the protocol version increments reflecting new patches are not expected to happen as a patch in the signature of an existing function would define new functionality.

## Compatibility matrix

The following matrix summarizes the compatibility between the versions of the Pantos protocol and the components of the Pantos ecosystem.

| Pantos Protocol | Ethereum Contracts | Service Node | Validator Node |
| ----  | ---- | ---- | ---- |
|       | 2.0.0 | 1.8.1 | 1.8.2 |
| 0.1.0 | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |

