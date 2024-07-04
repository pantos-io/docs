---
description: >-
  The PantosHub ABI is a JSON representation of the PantosHub smart contract's
  interface, containing the functions and events necessary for interacting with
  and managing cross-chain token registration
---

# PantosHub ABI

The ABI acts as an interface between the contract's bytecode and the outside world. Here's a breakdown of the important elements in the PantosHub ABI:

## Events

**ExternalTokenRegistered**: Emitted when an external token is registered on another blockchain.

**ExternalTokenUnregistered**: Emitted when an external token is unregistered from another blockchain.

**TokenRegistered**: Emitted when a token is registered on the current blockchain.

**TokenUnregistered**: Emitted when a token is unregistered from the current blockchain.

## Functions

**getPantosForwarder**: A view function that returns the address of the Pantos Forwarder, which is required for cross-chain functionality.

**registerExternalToken**: A nonpayable function that registers an external token from another blockchain to the Pantos Hub. It takes three arguments:

1. token: The address of the token on the current blockchain.
2. blockchainId: The ID of the blockchain where the external token resides.
3. externalToken: The address of the token on the external blockchain.

**registerToken**: A nonpayable function that registers a token to the Pantos Hub. It takes two arguments:

1. token: The address of the token to be registered.
2. stake: The amount of PAN tokens to be staked for registration (1000 PAN is required).

**unregisterExternalToken**: A nonpayable function that unregisters an external token from another blockchain. It takes two arguments:

1. token: The address of the token on the current blockchain.
2. blockchainId: The ID of the blockchain where the external token resides.

**unregisterToken**: A nonpayable function that unregisters a token from the Pantos Hub. It takes one argument:

1. token: The address of the token to be unregistered.

**getExternalTokenRecord:** A function to read the external token record for a registered token and a blockchain id. It takes two arguments:

1. token: The address of the token on the current blockchain.
2. blockchainId: The id of the external blockchain.

### PantosHub ABI JSON

```json
{
  "abi": [
    {
      "anonymous": false,
      "inputs": [
        {
          "indexed": false,
          "internalType": "address",
          "name": "token",
          "type": "address"
        },
        {
          "indexed": false,
          "internalType": "uint256",
          "name": "blockchainId",
          "type": "uint256"
        }
      ],
      "name": "ExternalTokenRegistered",
      "type": "event"
    },
    {
      "anonymous": false,
      "inputs": [
        {
          "indexed": false,
          "internalType": "address",
          "name": "token",
          "type": "address"
        },
        {
          "indexed": false,
          "internalType": "uint256",
          "name": "blockchainId",
          "type": "uint256"
        }
      ],
      "name": "ExternalTokenUnregistered",
      "type": "event"
    },
    {
      "anonymous": false,
      "inputs": [
        {
          "indexed": false,
          "internalType": "address",
          "name": "token",
          "type": "address"
        }
      ],
      "name": "TokenRegistered",
      "type": "event"
    },
    {
      "anonymous": false,
      "inputs": [
        {
          "indexed": false,
          "internalType": "address",
          "name": "token",
          "type": "address"
        }
      ],
      "name": "TokenUnregistered",
      "type": "event"
    },
    {
      "inputs": [],
      "name": "getPantosForwarder",
      "outputs": [
        {
          "internalType": "address",
          "name": "",
          "type": "address"
        }
      ],
      "stateMutability": "view",
      "type": "function"
    },
    {
      "inputs": [
        {
          "internalType": "address",
          "name": "token",
          "type": "address"
        },
        {
          "internalType": "uint256",
          "name": "blockchainId",
          "type": "uint256"
        },
        {
          "internalType": "string",
          "name": "externalToken",
          "type": "string"
        }
      ],
      "name": "registerExternalToken",
      "outputs": [],
      "stateMutability": "nonpayable",
      "type": "function"
    },
    {
      "inputs": [
        {
          "internalType": "address",
          "name": "token",
          "type": "address"
        },
        {
          "internalType": "uint256",
          "name": "stake",
          "type": "uint256"
        }
      ],
      "name": "registerToken",
      "outputs": [],
      "stateMutability": "nonpayable",
      "type": "function"
    },
    {
      "inputs": [
        {
          "internalType": "address",
          "name": "token",
          "type": "address"
        },
        {
          "internalType": "uint256",
          "name": "blockchainId",
          "type": "uint256"
        }
      ],
      "name": "unregisterExternalToken",
      "outputs": [],
      "stateMutability": "nonpayable",
      "type": "function"
    },
    {
      "inputs": [
        {
          "internalType": "address",
          "name": "token",
          "type": "address"
        }
      ],
      "name": "unregisterToken",
      "outputs": [],
      "stateMutability": "nonpayable",
      "type": "function"
    },
    {
      "inputs": [
        {
          "internalType": "address",
          "name": "token",
          "type": "address"
        },
        {
          "internalType": "uint256",
          "name": "blockchainId",
          "type": "uint256"
        }
      ],
      "name": "getExternalTokenRecord",
      "outputs": [
        {
          "components": [
            {
              "internalType": "bool",
              "name": "active",
              "type": "bool"
            },
            {
              "internalType": "string",
              "name": "externalToken",
              "type": "string"
            }
          ],
          "internalType": "struct PantosTypes.ExternalTokenRecord",
          "name": "",
          "type": "tuple"
        }
      ],
      "stateMutability": "view",
      "type": "function"
    }
  ]
}

```
