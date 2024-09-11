---
description: This is a resume of compatibility between the components of the Pantos ecosystem.
---

# Compatibility between versions

## The Pantos ecosystem

The Pantos ecosystem is composed of:
- [Pantos protocol](https://github.com/pantos-io/ethereum-contracts)
  
  A collection of smart contracts implementing the Pantos protocol.

- [Service Node](https://github.com/pantos-io/servicenode)
  
  A baseline implementation of a node interacting with the Pantos protocol and the multiple supported blockchains.

- [Validator Node](https://github.com/pantos-io/validatornode)

  A node responsible for validating cross-chain transfers on behalf of the users.

The Service Node interacts with the Pantos protocol to initiate cross-chain transfers. In order to do so, the Service Node needs to be compatible with the current version of the Pantos protocol. The following matrix summarizes the compatibility between the versions of the Pantos protocol and the Service Node.

| Pantos protocol / Service Node | 1.8.1 |
| ----| ---- |
| 1.2.1 | :heavy_check_mark: |

