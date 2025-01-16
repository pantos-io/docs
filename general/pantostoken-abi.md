# Pantos Token ABI

The Pantos Token ABI is a JSON representation of the `PantosToken` smart contract's interface, containing the functions and events necessary for interacting with cross-chain tokens.

The ABI acts as an interface between the contract's bytecode and the outside world. Here's a breakdown of the important elements in the Pantos Token ABI.

## Functions

### pantosTransfer

Called by the Pantos Forwarder to transfer tokens on a
blockchain.

*The function is only callable by a trusted Pantos Forwarder
contract and thefore can't be invoked by a user. The function is used
to transfer tokens on a blockchain between the sender and recipient.
Revert if anything prevents the transfer from happening.*


```solidity
function pantosTransfer(address sender, address recipient, uint256 amount)
    external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender`|`address`|The address of the sender of the tokens.|
|`recipient`|`address`|The address of the recipient of the tokens.|
|`amount`|`uint256`|The amount of tokens to mint.|


### pantosTransferFrom

Called by the Pantos Forwarder to debit tokens on the source
blockchain during a cross-chain transfer.

*The function is only callable by a trusted Pantos Forwarder
contract and thefore can't be invoked by a user. The function is used
to burn tokens on the source blockchain to initiate a cross-chain
transfer.
Revert if anything prevents the transfer from happening.*


```solidity
function pantosTransferFrom(address sender, uint256 amount) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender`|`address`|The address of the sender of the tokens.|
|`amount`|`uint256`|The amount of tokens to send/burn.|


### pantosTransferTo

Called by the Pantos Forwarder to mint tokens on the destination
blockchain during a cross-chain transfer.

*The function is only callable by a trusted Pantos Forwarder
contract and thefore can't be invoked by a user. The function is used
to mint tokens on the destination blockchain to finish a cross-chain
transfer.
Revert if anything prevents the transfer from happening.*


```solidity
function pantosTransferTo(address recipient, uint256 amount) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`recipient`|`address`|The address of the recipient of the tokens.|
|`amount`|`uint256`|The amount of tokens to mint.|


### getPantosForwarder

Returns the address of the Pantos Forwarder contract.


```solidity
function getPantosForwarder() external view returns (address);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|Address of the Pantos Forwarder.|

### totalSupply

*Returns the value of tokens in existence.*


```solidity
function totalSupply() external view returns (uint256);
```

### balanceOf

*Returns the value of tokens owned by `account`.*


```solidity
function balanceOf(address account) external view returns (uint256);
```

### transfer

*Moves a `value` amount of tokens from the caller's account to `to`.
Returns a boolean value indicating whether the operation succeeded.
Emits a [Transfer](/contracts/token/ERC20/IERC20.sol/interface.IERC20.md#transfer) event.*


```solidity
function transfer(address to, uint256 value) external returns (bool);
```

### allowance

*Returns the remaining number of tokens that `spender` will be
allowed to spend on behalf of `owner` through [transferFrom](/contracts/token/ERC20/IERC20.sol/interface.IERC20.md#transferfrom). This is
zero by default.
This value changes when {approve} or {transferFrom} are called.*


```solidity
function allowance(address owner, address spender) external view returns (uint256);
```

### approve

*Sets a `value` amount of tokens as the allowance of `spender` over the
caller's tokens.
Returns a boolean value indicating whether the operation succeeded.
IMPORTANT: Beware that changing an allowance with this method brings the risk
that someone may use both the old and the new allowance by unfortunate
transaction ordering. One possible solution to mitigate this race
condition is to first reduce the spender's allowance to 0 and set the
desired value afterwards:
https://github.com/ethereum/EIPs/issues/20#issuecomment-263524729
Emits an [Approval](/contracts/token/ERC20/IERC20.sol/interface.IERC20.md#approval) event.*


```solidity
function approve(address spender, uint256 value) external returns (bool);
```

### transferFrom

*Moves a `value` amount of tokens from `from` to `to` using the
allowance mechanism. `value` is then deducted from the caller's
allowance.
Returns a boolean value indicating whether the operation succeeded.
Emits a [Transfer](/contracts/token/ERC20/IERC20.sol/interface.IERC20.md#transfer) event.*


```solidity
function transferFrom(address from, address to, uint256 value) external returns (bool);
```

### decimals


```solidity
function decimals() external view returns (uint8);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint8`|The token decimals.|


### symbol


```solidity
function symbol() external view returns (string memory);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`string`|The token symbol.|


### name


```solidity
function name() external view returns (string memory);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`string`|The token name.|


### getOwner


```solidity
function getOwner() external view returns (address);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|The token owner.|

### supportsInterface

*Returns true if this contract implements the interface defined by
`interfaceId`. See the corresponding
https://eips.ethereum.org/EIPS/eip-165#how-interfaces-are-identified[EIP section]
to learn more about how these ids are created.
This function call must use less than 30 000 gas.*


```solidity
function supportsInterface(bytes4 interfaceId) external view returns (bool);
```

## Events

### PantosForwarderSet

```solidity
event PantosForwarderSet(address pantosForwarder);
```

### PantosForwarderUnset

```solidity
event PantosForwarderUnset();
```

### Transfer
*Emitted when `value` tokens are moved from one account (`from`) to
another (`to`).
Note that `value` may be zero.*


```solidity
event Transfer(address indexed from, address indexed to, uint256 value);
```

### Approval
*Emitted when the allowance of a `spender` for an `owner` is set by
a call to [approve](/contracts/token/ERC20/IERC20.sol/interface.IERC20.md#approve). `value` is the new allowance.*


```solidity
event Approval(address indexed owner, address indexed spender, uint256 value);
```

## ABI

```json
[
  {
    "type": "function",
    "name": "allowance",
    "inputs": [
      {
        "name": "owner",
        "type": "address",
        "internalType": "address"
      },
      {
        "name": "spender",
        "type": "address",
        "internalType": "address"
      }
    ],
    "outputs": [
      {
        "name": "",
        "type": "uint256",
        "internalType": "uint256"
      }
    ],
    "stateMutability": "view"
  },
  {
    "type": "function",
    "name": "approve",
    "inputs": [
      {
        "name": "spender",
        "type": "address",
        "internalType": "address"
      },
      {
        "name": "value",
        "type": "uint256",
        "internalType": "uint256"
      }
    ],
    "outputs": [
      {
        "name": "",
        "type": "bool",
        "internalType": "bool"
      }
    ],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "balanceOf",
    "inputs": [
      {
        "name": "account",
        "type": "address",
        "internalType": "address"
      }
    ],
    "outputs": [
      {
        "name": "",
        "type": "uint256",
        "internalType": "uint256"
      }
    ],
    "stateMutability": "view"
  },
  {
    "type": "function",
    "name": "decimals",
    "inputs": [],
    "outputs": [
      {
        "name": "",
        "type": "uint8",
        "internalType": "uint8"
      }
    ],
    "stateMutability": "view"
  },
  {
    "type": "function",
    "name": "getOwner",
    "inputs": [],
    "outputs": [
      {
        "name": "",
        "type": "address",
        "internalType": "address"
      }
    ],
    "stateMutability": "view"
  },
  {
    "type": "function",
    "name": "getPantosForwarder",
    "inputs": [],
    "outputs": [
      {
        "name": "",
        "type": "address",
        "internalType": "address"
      }
    ],
    "stateMutability": "view"
  },
  {
    "type": "function",
    "name": "name",
    "inputs": [],
    "outputs": [
      {
        "name": "",
        "type": "string",
        "internalType": "string"
      }
    ],
    "stateMutability": "view"
  },
  {
    "type": "function",
    "name": "pantosTransfer",
    "inputs": [
      {
        "name": "sender",
        "type": "address",
        "internalType": "address"
      },
      {
        "name": "recipient",
        "type": "address",
        "internalType": "address"
      },
      {
        "name": "amount",
        "type": "uint256",
        "internalType": "uint256"
      }
    ],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "pantosTransferFrom",
    "inputs": [
      {
        "name": "sender",
        "type": "address",
        "internalType": "address"
      },
      {
        "name": "amount",
        "type": "uint256",
        "internalType": "uint256"
      }
    ],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "pantosTransferTo",
    "inputs": [
      {
        "name": "recipient",
        "type": "address",
        "internalType": "address"
      },
      {
        "name": "amount",
        "type": "uint256",
        "internalType": "uint256"
      }
    ],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "supportsInterface",
    "inputs": [
      {
        "name": "interfaceId",
        "type": "bytes4",
        "internalType": "bytes4"
      }
    ],
    "outputs": [
      {
        "name": "",
        "type": "bool",
        "internalType": "bool"
      }
    ],
    "stateMutability": "view"
  },
  {
    "type": "function",
    "name": "symbol",
    "inputs": [],
    "outputs": [
      {
        "name": "",
        "type": "string",
        "internalType": "string"
      }
    ],
    "stateMutability": "view"
  },
  {
    "type": "function",
    "name": "totalSupply",
    "inputs": [],
    "outputs": [
      {
        "name": "",
        "type": "uint256",
        "internalType": "uint256"
      }
    ],
    "stateMutability": "view"
  },
  {
    "type": "function",
    "name": "transfer",
    "inputs": [
      {
        "name": "to",
        "type": "address",
        "internalType": "address"
      },
      {
        "name": "value",
        "type": "uint256",
        "internalType": "uint256"
      }
    ],
    "outputs": [
      {
        "name": "",
        "type": "bool",
        "internalType": "bool"
      }
    ],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "transferFrom",
    "inputs": [
      {
        "name": "from",
        "type": "address",
        "internalType": "address"
      },
      {
        "name": "to",
        "type": "address",
        "internalType": "address"
      },
      {
        "name": "value",
        "type": "uint256",
        "internalType": "uint256"
      }
    ],
    "outputs": [
      {
        "name": "",
        "type": "bool",
        "internalType": "bool"
      }
    ],
    "stateMutability": "nonpayable"
  },
  {
    "type": "event",
    "name": "Approval",
    "inputs": [
      {
        "name": "owner",
        "type": "address",
        "indexed": true,
        "internalType": "address"
      },
      {
        "name": "spender",
        "type": "address",
        "indexed": true,
        "internalType": "address"
      },
      {
        "name": "value",
        "type": "uint256",
        "indexed": false,
        "internalType": "uint256"
      }
    ],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "PantosForwarderSet",
    "inputs": [
      {
        "name": "pantosForwarder",
        "type": "address",
        "indexed": false,
        "internalType": "address"
      }
    ],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "PantosForwarderUnset",
    "inputs": [],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "Transfer",
    "inputs": [
      {
        "name": "from",
        "type": "address",
        "indexed": true,
        "internalType": "address"
      },
      {
        "name": "to",
        "type": "address",
        "indexed": true,
        "internalType": "address"
      },
      {
        "name": "value",
        "type": "uint256",
        "indexed": false,
        "internalType": "uint256"
      }
    ],
    "anonymous": false
  }
]
```
