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

If not stated otherwise, deployed components (Service and Validator nodes) MUST only interact with the latest deployed available version of the Pantos Protocol. The smart contracts offer an existing function to check the currently available version. 

## Compatibility matrix

The following matrix summarizes the compatibility between the versions of the Pantos protocol and the Service Node.

| Service Node / Pantos Protocol | 0.1.0 |
| ----| ---- |
| 1.8.1 | :heavy_check_mark: |

