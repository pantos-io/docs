# Pantos Hub ABI

The Pantos Hub ABI is a JSON representation of the `PantosHub` smart contract's interface, containing the functions and events necessary to register tokens and service nodes, and to submit cross-chain token transfers.

The ABI acts as an interface between the contract's bytecode and the outside world. Here's a breakdown of the important elements in the Pantos Hub ABI.

## Functions

### pause

Pauses the Pantos Hub.

*The function can only be called by the pauser role
and only if the contract is not paused.*


```solidity
function pause() external;
```

### unpause

Unpauses the Pantos Hub.

*The function can only be called by the super critical ops role
and only if the contract is paused.*


```solidity
function unpause() external;
```

### setPantosForwarder

Sets the Pantos Forwarder contract address.

*The function can only be called by the super critical ops role
and only if the contract is paused.*


```solidity
function setPantosForwarder(address pantosForwarder) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`pantosForwarder`|`address`|The address of the Pantos Forwarder contract.|


### setPantosToken

Set the Pantos Token contract address.

*The function can only be called by the super critical ops
role and only if the contract is paused.*


```solidity
function setPantosToken(address pantosToken) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`pantosToken`|`address`|The address of the Pantos Token contract.|


### setPrimaryValidatorNode

Update the primary validator node.

*The function can only be called by the super critical ops role
and only if the contract is paused.*


```solidity
function setPrimaryValidatorNode(address primaryValidatorNodeAddress)
    external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`primaryValidatorNodeAddress`|`address`|The address of the primary validator node.|


### registerBlockchain

Used by the super critical ops role to register a new
blockchain.

*The function can only be called by the super critical ops role.*


```solidity
function registerBlockchain(
    uint256 blockchainId,
    string calldata name,
    uint256 validatorFeeFactor
) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`blockchainId`|`uint256`|The ID of the new blockchain.|
|`name`|`string`|The name of the new blockchain.|
|`validatorFeeFactor`|`uint256`|The validator fee factor of the new blockchain.|


### unregisterBlockchain

Used by the super critical ops role to unregister a
blockchain.


```solidity
function unregisterBlockchain(uint256 blockchainId) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`blockchainId`|`uint256`|The id of the blockchain to be unregistered.|


### updateBlockchainName

Used by the medium critical ops role to update the name
of a registered blockchain.

*The function can only be called by the medium critical ops role
and if the contract is paused.*


```solidity
function updateBlockchainName(uint256 blockchainId, string calldata name)
    external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`blockchainId`|`uint256`|The id of the blockchain to be updated.|
|`name`|`string`|The new name of the blockchain.|


### initiateValidatorFeeFactorUpdate

Initiate an update of a validator fee factor.

*The function can only be called by the medium critical ops role.*


```solidity
function initiateValidatorFeeFactorUpdate(
    uint256 blockchainId,
    uint256 newValidatorFeeFactor
) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`blockchainId`|`uint256`|The ID of the blockchain the validator fee factor is updated for.|
|`newValidatorFeeFactor`|`uint256`|The new validator fee factor.|


### executeValidatorFeeFactorUpdate

Execute an update of a validator fee factor.

*The function can only be called when the time delay after
an initiated update has elapsed.*


```solidity
function executeValidatorFeeFactorUpdate(uint256 blockchainId) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`blockchainId`|`uint256`|The ID of the blockchain the validator fee factor is updated for.|


### initiateUnbondingPeriodServiceNodeDepositUpdate

Initiate an update of the unbonding period for service
node deposits.

*The function can only be called by the medium critical ops role.*


```solidity
function initiateUnbondingPeriodServiceNodeDepositUpdate(
    uint256 newUnbondingPeriodServiceNodeDeposit
) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newUnbondingPeriodServiceNodeDeposit`|`uint256`|The new unbonding period (in seconds) for service node deposits.|


### executeUnbondingPeriodServiceNodeDepositUpdate

Execute an update of the unbonding period for service
node deposits.

*The function can only be called when the time delay after
an initiated update has elapsed.*


```solidity
function executeUnbondingPeriodServiceNodeDepositUpdate() external;
```

### initiateMinimumServiceNodeDepositUpdate

Initiate an update of the minimum service node deposit.

*The function can only be called by the medium critical ops role.*


```solidity
function initiateMinimumServiceNodeDepositUpdate(
    uint256 newMinimumServiceNodeDeposit
) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newMinimumServiceNodeDeposit`|`uint256`|The new minimum service node deposit.|


### executeMinimumServiceNodeDepositUpdate

Execute an update of the minimum service node deposit.

*The function can only be called when the time delay after
an initiated update has elapsed.*


```solidity
function executeMinimumServiceNodeDepositUpdate() external;
```

### initiateParameterUpdateDelayUpdate

Initiate an update of the parameter update delay.

*The function can only be called by the medium critical ops role.*


```solidity
function initiateParameterUpdateDelayUpdate(uint256 newParameterUpdateDelay)
    external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newParameterUpdateDelay`|`uint256`|The new parameter update delay.|


### executeParameterUpdateDelayUpdate

Execute an update of the parameter update delay.

*The function can only be called when the time delay after
an initiated update has elapsed.*


```solidity
function executeParameterUpdateDelayUpdate() external;
```

### registerToken

Allows a user to register a token with the Pantos Hub. The user
is required to be the owner of the token contract.


```solidity
function registerToken(address token) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token`|`address`|The address of the token contract.|


### unregisterToken

Allows a user to unregister a token with the Pantos Hub. The
user is required to be the owner of the token contract.


```solidity
function unregisterToken(address token) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token`|`address`|The address of the token contract.|


### registerExternalToken

Allows a user to register an external token with the Pantos Hub.
The external token is a token contract on another blockchain.

*The owner of a token residing on the current blockchain can register
an external token with the Pantos Hub. The external token is a token
contract on another blockchain. The external token is required to be
deployed on the blockchain with the given id. The external token is
required to be registered with the Pantos Hub on the blockchain with the
given id.*


```solidity
function registerExternalToken(
    address token,
    uint256 blockchainId,
    string calldata externalToken
) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token`|`address`|The address of the token contract on the current blockchain.|
|`blockchainId`|`uint256`|The id of the blockchain on which the external token is deployed.|
|`externalToken`|`string`|The address of the token contract on the external blockchain.|


### unregisterExternalToken

Allows a user to unregister an external token from the Pantos Hub
on the current blockchain. The external token is a token contract on
another blockchain. Unregistering an external token from the Pantos Hub
makes it impossible to transfer tokens between the current blockchain and
the blockchain on which the external token is deployed.

*The owner of a token residing on the current blockchain can
unregister an external token from the Pantos Hub. The external token is a
token contract on another blockchain. The external token is required to
be deployed on the blockchain with the given id. The external token is
required to be registered with the Pantos Hub on the blockchain with the
given id. Unregistering an external token from the Pantos Hub makes it
impossible to transfer tokens between the current blockchain and the
blockchain on which the external token is deployed.*


```solidity
function unregisterExternalToken(address token, uint256 blockchainId)
    external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token`|`address`|The address of the token contract on the current blockchain.|
|`blockchainId`|`uint256`|The id of the blockchain on which the external token is deployed.|


### registerServiceNode

Used by a service node or its withdrawal address to
register a service node at the Pantos Hub.

*The function is only callable by a service node itself or its
withdrawal address. The service node is required to provide a URL
under which it is reachable. The service node is required to provide
a deposit in PAN in order to register. The deposit is required to be at
least the minimum service node deposit. The service node is required
to provide a withdrawal address where the deposit will be returned
after the unregistration and the elapse of the unbonding period.
The service node is required to be registered at the Pantos Hub in
order to be able to transfer tokens between blockchains.
If the service node was unregistered, this function can be called
only if the deposit has already been withdrawn. If the service node
intends to register again after an uregistration but the deposit has
not been withdrawn, use the cancelServiceNodeUnregistration function.*


```solidity
function registerServiceNode(
    address serviceNodeAddress,
    string calldata url,
    uint256 deposit,
    address withdrawalAddress
) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`serviceNodeAddress`|`address`|The registered service node address.|
|`url`|`string`|The URL under which the service node is reachable.|
|`deposit`|`uint256`|The provided deposit in PAN.|
|`withdrawalAddress`|`address`|The address where the deposit will be returned to after the service node has been unregistered.|


### unregisterServiceNode

Used by a service node or its withdrawal address to
unregister a service node from the Pantos Hub.

*The function is only callable by a service node itself or its
withdrawal address. The service node is required to be registered in
the Pantos Hub in order to be able to transfer tokens between
blockchains. Unregistering a service node from the Pantos Hub makes
it impossible to transfer tokens between blockchains using the
service node. The deposit of the service node can be withdrawn after
the elapse of the unbonding period by calling the
withdrawServiceNodeDeposit function at the PantosHub.*


```solidity
function unregisterServiceNode(address serviceNodeAddress) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`serviceNodeAddress`|`address`|The address of the service node which is unregistered.|


### withdrawServiceNodeDeposit

Used by a service node or its withdrawal address to
withdraw the deposit from the Pantos Hub.

*The function is only callable by a service node itself or its
withdrawal address. The deposit can be withdrawn only if the unbonding
period has elapsed. The unbonding period is the minimum time that
must pass between the unregistration of the service node and the
withdrawal of the deposit.*


```solidity
function withdrawServiceNodeDeposit(address serviceNodeAddress) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`serviceNodeAddress`|`address`|The address of the service node which wants to withdraw its deposit.|


### cancelServiceNodeUnregistration

Used by a service node or its withdrawal address to cancel
the unregistration from the PantosHub.

*The function is only callable by a service node itself or its
withdrawal address. A service node might need to have its unregistration
cancelled if a new registration is required before the unbondoing
period would elapse.*


```solidity
function cancelServiceNodeUnregistration(address serviceNodeAddress)
    external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`serviceNodeAddress`|`address`|The address of the service node to cancel the unregistration for.|


### increaseServiceNodeDeposit

Increase a service node's deposit at the Pantos Hub.

*The function is only callable by an active service node
itself or the account of its withdrawal address.*


```solidity
function increaseServiceNodeDeposit(
    address serviceNodeAddress,
    uint256 deposit
) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`serviceNodeAddress`|`address`|The address of the service node which will have its deposit increased.|
|`deposit`|`uint256`|The amount that will be added to the current deposit of the service node.|


### decreaseServiceNodeDeposit

Decrease a service node's deposit at the Pantos Hub.

*The function is only callable by an active service node
itself or the account of its withdrawal address.*


```solidity
function decreaseServiceNodeDeposit(
    address serviceNodeAddress,
    uint256 deposit
) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`serviceNodeAddress`|`address`|The address of the service node which will have its deposit decreased.|
|`deposit`|`uint256`|The amount that will be subtracted from the current deposit of the service node.|


### updateServiceNodeUrl

Used by a service node to update its url in the Pantos Hub.

*The function is only callable by a service node itself.
The service node is required to provide a new unique url under which it
is reachable.*


```solidity
function updateServiceNodeUrl(string calldata url) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`url`|`string`|The new url as string.|


### getPantosForwarder

Returns the address of the Pantos Forwarder contract.


```solidity
function getPantosForwarder() external view returns (address);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|The address of the Pantos Forwarder contract.|


### getPantosToken

Returns the address of the Pantos Token contract.


```solidity
function getPantosToken() external view returns (address);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|The address of the Pantos Token contract.|


### getPrimaryValidatorNode


```solidity
function getPrimaryValidatorNode() external view returns (address);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|The address of the primary validator node.|


### getNumberBlockchains

Returns the number of blockchains registered with the Pantos Hub.


```solidity
function getNumberBlockchains() external view returns (uint256);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The number as uint of blockchains registered with the Pantos Hub.|


### getNumberActiveBlockchains

Returns the number of active blockchains registered with the
Pantos Hub.


```solidity
function getNumberActiveBlockchains() external view returns (uint256);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The number as uint of active blockchains registered with the Pantos Hub.|


### getCurrentBlockchainId

Returns the blockchain id of the current blockchain.


```solidity
function getCurrentBlockchainId() external view returns (uint256);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The blockchain id as unit of the current blockchain.|


### getBlockchainRecord

Returns a blockchain record for a given blockchain id.

*More information about the blockchain record can be found at
[PantosTypes-BlockchainRecord](/src/interfaces/PantosTypes.sol/library.PantosTypes.md#blockchainrecord).*


```solidity
function getBlockchainRecord(uint256 blockchainId)
    external
    view
    returns (PantosTypes.BlockchainRecord memory);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`blockchainId`|`uint256`|The id of the blockchain.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`PantosTypes.BlockchainRecord`|The blockchain record for the given blockchain id.|


### getCurrentMinimumServiceNodeDeposit


```solidity
function getCurrentMinimumServiceNodeDeposit()
    external
    view
    returns (uint256);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The current minimum required deposit to register a service node at the Pantos Hub.|


### getMinimumServiceNodeDeposit


```solidity
function getMinimumServiceNodeDeposit()
    external
    view
    returns (PantosTypes.UpdatableUint256 memory);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`PantosTypes.UpdatableUint256`|All data related to the minimum required deposit to register a service node at the Pantos Hub.|


### getCurrentUnbondingPeriodServiceNodeDeposit


```solidity
function getCurrentUnbondingPeriodServiceNodeDeposit()
    external
    view
    returns (uint256);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The current unbonding period (in seconds) for service node deposits.|


### getUnbondingPeriodServiceNodeDeposit


```solidity
function getUnbondingPeriodServiceNodeDeposit()
    external
    view
    returns (PantosTypes.UpdatableUint256 memory);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`PantosTypes.UpdatableUint256`|All data related to the unbonding period (in seconds) for service node deposits.|


### getTokens

Returns a list of all tokens registered in the Pantos Hub which
are also deployed on the same blockchain as this Pantos Hub.


```solidity
function getTokens() external view returns (address[] memory);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address[]`|A list of addresses of tokens registered in the Pantos Hub.|


### getTokenRecord

Returns a token record for a given token address.

*More information about the TokenRecord data structure can be found
at [PantosTypes-TokenRecord](/src/interfaces/PantosTypes.sol/library.PantosTypes.md#tokenrecord).*


```solidity
function getTokenRecord(address token)
    external
    view
    returns (PantosTypes.TokenRecord memory);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token`|`address`|The address of a registered token for which a token record is requested.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`PantosTypes.TokenRecord`|A TokenRecord data structure.|


### getExternalTokenRecord

Returns a external token record for a external token under the
given token address and blockchain id.

*More information about the ExternalTokenRecord data structure can
be found [PantosTypes-ExternalTokenRecord](/src/interfaces/PantosTypes.sol/library.PantosTypes.md#externaltokenrecord).*


```solidity
function getExternalTokenRecord(address token, uint256 blockchainId)
    external
    view
    returns (PantosTypes.ExternalTokenRecord memory);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token`|`address`|The address of the token registered in the Pantos Hub and being deployed on the same chain as the Pantos Hub.|
|`blockchainId`|`uint256`|The blockchain id of a different blockchain on which the external token is deployed too.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`PantosTypes.ExternalTokenRecord`|A ExternalTokenRecord data structure.|


### getServiceNodes

Returns a list of registered service nodes.


```solidity
function getServiceNodes() external view returns (address[] memory);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address[]`|A list of addresses of registered services nodes.|


### getServiceNodeRecord

Returns a service node record for a given service node address.

*More information about the ServiceNodeRecord data structure can be
found at [PantosTypes-ServiceNodeRecord](/src/interfaces/PantosTypes.sol/library.PantosTypes.md#servicenoderecord).*


```solidity
function getServiceNodeRecord(address serviceNode)
    external
    view
    returns (PantosTypes.ServiceNodeRecord memory);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`serviceNode`|`address`|The address of a registered service node.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`PantosTypes.ServiceNodeRecord`|A ServiceNodeRecord data structure.|


### getCurrentValidatorFeeFactor


```solidity
function getCurrentValidatorFeeFactor(uint256 blockchainId)
    external
    view
    returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`blockchainId`|`uint256`|The ID of the blockchain to get the validator fee factor for.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The current validator fee factor for the given blockchain.|


### getValidatorFeeFactor


```solidity
function getValidatorFeeFactor(uint256 blockchainId)
    external
    view
    returns (PantosTypes.UpdatableUint256 memory);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`blockchainId`|`uint256`|The ID of the blockchain to get the validator fee factor for.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`PantosTypes.UpdatableUint256`|All data related to the validator fee factor for the given blockchain.|


### getCurrentParameterUpdateDelay


```solidity
function getCurrentParameterUpdateDelay() external view returns (uint256);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The current time delay for updating Pantos Hub parameters.|


### getParameterUpdateDelay


```solidity
function getParameterUpdateDelay()
    external
    view
    returns (PantosTypes.UpdatableUint256 memory);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`PantosTypes.UpdatableUint256`|All data related to the time delay for updating Pantos Hub parameters.|


### isServiceNodeInTheUnbondingPeriod

Takes the service node address and returns whether the
service node is in the unbonding period or not.


```solidity
function isServiceNodeInTheUnbondingPeriod(address serviceNodeAddress)
    external
    view
    returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`serviceNodeAddress`|`address`|The service node address to be checked.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|True if the service node is in the unbonding period, false otherwise.|


### isValidValidatorNodeNonce

Check if a given nonce is a valid (i.e. not yet used)
validator node nonce.


```solidity
function isValidValidatorNodeNonce(uint256 nonce)
    external
    view
    returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`nonce`|`uint256`|The nonce to be checked.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|True if the nonce is valid.|


### paused

*Returns true if the contract is paused, and false otherwise.*


```solidity
function paused() external view returns (bool);
```

### transfer

Transfers token between from a sender to a recipient on the
current blockchain. This function can only be called by an active
service node

*The function is only callable by an active service node. The
transfer request is required to be valid and signed by the sender of
the tokens. More information about the TransferRequest data structure
can be found at [PantosTypes-TransferRequest](/src/interfaces/PantosTypes.sol/library.PantosTypes.md#transferrequest)*


```solidity
function transfer(
    PantosTypes.TransferRequest calldata request,
    bytes memory signature
) external returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`request`|`PantosTypes.TransferRequest`|The TransferRequest data structure containing the transfer request on the current blockchain|
|`signature`|`bytes`|Signature over the transfer request from the sender|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The id of the transfer|


### transferFrom

Sender initiates a token transfer from the current blockchain to
a recipient on another blockchain. This function can only be called by
an active service node

*The function is only callable by an active service node. The
transfer request is required to be valid and signed by the sender of
the tokens. The senders tokens are burnt on the current blockchain.
More information about the TransferFromRequest data structure can be
found at [PantosTypes-TransferFromRequest](/src/interfaces/PantosTypes.sol/library.PantosTypes.md#transferfromrequest)*


```solidity
function transferFrom(
    PantosTypes.TransferFromRequest calldata request,
    bytes memory signature
) external returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`request`|`PantosTypes.TransferFromRequest`|The TransferFromRequest data structure containing the transfer request across blockchains|
|`signature`|`bytes`|Signature over the transfer request from the sender|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The id of the transfer|


### transferTo

Second step of a cross-blockchain token transfer. The function
is called by the Pantos Validator on the destination blockchain and
the tokens are minted into the recipients wallet.

*The function is only callable by the Pantos Validator on the
destination blockchain. The transfer request is required to be valid and
signed by the Pantos Validator. The tokens are minted into the
recipients address on the destination blockchain. More information about
the TransferToRequest data structure can be found at
[PantosTypes-TransferToRequest](/src/interfaces/PantosTypes.sol/library.PantosTypes.md#transfertorequest).*


```solidity
function transferTo(
    PantosTypes.TransferToRequest calldata request,
    address[] memory signerAddresses,
    bytes[] memory signatures
) external returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`request`|`PantosTypes.TransferToRequest`|The TransferToRequest data structure containing the transfer request across blockchains.|
|`signerAddresses`|`address[]`|The addresses of the validator nodes that signed the transfer (must be ordered from the lowest to the highest address).|
|`signatures`|`bytes[]`|The signatures of the validator nodes (each signature must be in the same array position as the corresponding signer address).|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The ID of the transfer.|


### isValidSenderNonce

Takes a sender address and a nonce and returns whether the nonce
is valid for the sender or not


```solidity
function isValidSenderNonce(address sender, uint256 nonce)
    external
    view
    returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender`|`address`|The address of the sender|
|`nonce`|`uint256`|The nonce to be checked|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|True if the nonce is valid, false otherwise|


### verifyTransfer

Verifies if a TransferRequest data structure is valid or not

*The function reverts if the TransferRequest data structure is not
valid*


```solidity
function verifyTransfer(
    PantosTypes.TransferRequest calldata request,
    bytes memory signature
) external view;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`request`|`PantosTypes.TransferRequest`|The TransferRequest data structure to be checked|
|`signature`|`bytes`|The signature over the TransferRequest data structure|


### verifyTransferFrom

Verifies if a TransferFromRequest data structure is valid or not

*The function reverts if the TransferFromRequest data structure is
not valid*


```solidity
function verifyTransferFrom(
    PantosTypes.TransferFromRequest calldata request,
    bytes memory signature
) external view;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`request`|`PantosTypes.TransferFromRequest`|The TransferFromRequest data structure to be checked|
|`signature`|`bytes`|The signature over the TransferFromRequest data|


### verifyTransferTo

Verifies if a TransferToRequest data structure is valid or not.

*The function reverts if the TransferToRequest data structure is not
valid.*


```solidity
function verifyTransferTo(
    PantosTypes.TransferToRequest calldata request,
    address[] memory signerAddresses,
    bytes[] memory signatures
) external view;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`request`|`PantosTypes.TransferToRequest`|The TransferToRequest data structure to be checked.|
|`signerAddresses`|`address[]`|The addresses of the validator nodes that signed the transfer (must be ordered from the lowest to the highest address).|
|`signatures`|`bytes[]`|The signatures of the validator nodes (each signature must be in the same array position as the corresponding signer address).|


### getNextTransferId

*This function returns a transfer id to be used in next transfer.*


```solidity
function getNextTransferId() external view returns (uint256);
```

## Events

### Paused

```solidity
event Paused(address account);
```

### Unpaused

```solidity
event Unpaused(address account);
```

### PantosForwarderSet

```solidity
event PantosForwarderSet(address pantosForwarder);
```

### PantosTokenSet

```solidity
event PantosTokenSet(address pantosToken);
```

### PrimaryValidatorNodeUpdated
Event that is emitted when the primary validator node is
updated.


```solidity
event PrimaryValidatorNodeUpdated(address primaryValidatorNodeAddress);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`primaryValidatorNodeAddress`|`address`|The address of the primary validator node.|

### BlockchainRegistered
Event that is emitted when a new blockchain is
registered.


```solidity
event BlockchainRegistered(uint256 blockchainId, uint256 validatorFeeFactor);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`blockchainId`|`uint256`|The ID of the new blockchain.|
|`validatorFeeFactor`|`uint256`|The validator fee factor of the new blockchain.|

### BlockchainUnregistered
Event that is emitted when an already registered blockchain
is unregistered.


```solidity
event BlockchainUnregistered(uint256 blockchainId);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`blockchainId`|`uint256`|The id of the blockchain.|

### BlockchainNameUpdated

```solidity
event BlockchainNameUpdated(uint256 blockchainId);
```

### TokenRegistered

```solidity
event TokenRegistered(address token);
```

### TokenUnregistered

```solidity
event TokenUnregistered(address token);
```

### ExternalTokenRegistered

```solidity
event ExternalTokenRegistered(address token, uint256 blockchainId);
```

### ExternalTokenUnregistered

```solidity
event ExternalTokenUnregistered(address token, uint256 blockchainId);
```

### ServiceNodeRegistered
Event that is emitted when a new service node is registered.


```solidity
event ServiceNodeRegistered(address serviceNode);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`serviceNode`|`address`|The address of the new service node.|

### ServiceNodeUnregistered
Event that is emitted when a registered service node is
unregistered.


```solidity
event ServiceNodeUnregistered(address serviceNode);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`serviceNode`|`address`|The address of the registered service node.|

### ServiceNodeUrlUpdated
Event that is emitted when a registered service node url is
updated.


```solidity
event ServiceNodeUrlUpdated(address serviceNode);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`serviceNode`|`address`|The address of the registered service node.|

### UnbondingPeriodServiceNodeDepositUpdateInitiated
Event that is emitted when an update of the unbonding
period for service node deposits is initiated.


```solidity
event UnbondingPeriodServiceNodeDepositUpdateInitiated(
    uint256 newUnbondingPeriodServiceNodeDeposit, uint256 earliestUpdateTime
);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newUnbondingPeriodServiceNodeDeposit`|`uint256`|The new unbonding period (in seconds) for service node deposits.|
|`earliestUpdateTime`|`uint256`|The earliest time when the update can be executed.|

### UnbondingPeriodServiceNodeDepositUpdateExecuted
Event that is emitted when an update of the unbonding
period for service node deposits is executed.


```solidity
event UnbondingPeriodServiceNodeDepositUpdateExecuted(
    uint256 newUnbondingPeriodServiceNodeDeposit
);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newUnbondingPeriodServiceNodeDeposit`|`uint256`|The new unbonding period (in seconds) for service node deposits.|

### MinimumServiceNodeDepositUpdateInitiated
Event that is emitted when an update of the minimum
service node deposit is initiated.


```solidity
event MinimumServiceNodeDepositUpdateInitiated(
    uint256 newMinimumServiceNodeDeposit, uint256 earliestUpdateTime
);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newMinimumServiceNodeDeposit`|`uint256`|The new minimum service node deposit.|
|`earliestUpdateTime`|`uint256`|The earliest time when the update can be executed.|

### MinimumServiceNodeDepositUpdateExecuted
Event that is emitted when an update of the minimum
service node deposit is executed.


```solidity
event MinimumServiceNodeDepositUpdateExecuted(
    uint256 newMinimumServiceNodeDeposit
);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newMinimumServiceNodeDeposit`|`uint256`|The new minimum service node deposit.|

### ValidatorFeeFactorUpdateInitiated
Event that is emitted when an update of a validator fee
factor is initiated.


```solidity
event ValidatorFeeFactorUpdateInitiated(
    uint256 blockchainId,
    uint256 newValidatorFeeFactor,
    uint256 earliestUpdateTime
);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`blockchainId`|`uint256`|The ID of the blockchain the validator fee factor is updated for.|
|`newValidatorFeeFactor`|`uint256`|The new validator fee factor.|
|`earliestUpdateTime`|`uint256`|The earliest time when the update can be executed.|

### ValidatorFeeFactorUpdateExecuted
Event that is emitted when an update of a validator fee
factor is executed.


```solidity
event ValidatorFeeFactorUpdateExecuted(
    uint256 blockchainId, uint256 newValidatorFeeFactor
);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`blockchainId`|`uint256`|The ID of the blockchain the validator fee factor is updated for.|
|`newValidatorFeeFactor`|`uint256`|The new validator fee factor.|

### ParameterUpdateDelayUpdateInitiated
Event that is emitted when an update of the parameter
update delay is initiated.


```solidity
event ParameterUpdateDelayUpdateInitiated(
    uint256 newParameterUpdateDelay, uint256 earliestUpdateTime
);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newParameterUpdateDelay`|`uint256`|The new parameter update delay.|
|`earliestUpdateTime`|`uint256`|The earliest time when the update can be executed.|

### ParameterUpdateDelayUpdateExecuted
Event that is emitted when an update of the parameter
update delay is executed.


```solidity
event ParameterUpdateDelayUpdateExecuted(uint256 newParameterUpdateDelay);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newParameterUpdateDelay`|`uint256`|The new parameter update delay.|

### TransferSucceeded
Event that is emitted when a Pantos single-chain token
transfer succeeded.


```solidity
event TransferSucceeded(
    uint256 transferId, PantosTypes.TransferRequest request, bytes signature
);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`transferId`|`uint256`|The unique Pantos transfer ID on the blockchain.|
|`request`|`PantosTypes.TransferRequest`|The transfer request.|
|`signature`|`bytes`|The sender's signature.|

### TransferFailed
Event that is emitted when a Pantos single-chain token
transfer failed.


```solidity
event TransferFailed(
    uint256 transferId,
    PantosTypes.TransferRequest request,
    bytes signature,
    bytes32 tokenData
);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`transferId`|`uint256`|The unique Pantos transfer ID on the blockchain.|
|`request`|`PantosTypes.TransferRequest`|The transfer request.|
|`signature`|`bytes`|The sender's signature.|
|`tokenData`|`bytes32`|Optional PANDAS token data (may contain an error message).|

### TransferFromSucceeded
Event that is emitted when a Pantos cross-chain token
transfer succeeded on the source blockchain.


```solidity
event TransferFromSucceeded(
    uint256 sourceTransferId,
    PantosTypes.TransferFromRequest request,
    bytes signature
);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sourceTransferId`|`uint256`|The unique Pantos transfer ID on the source blockchain.|
|`request`|`PantosTypes.TransferFromRequest`|The transfer request.|
|`signature`|`bytes`|The sender's signature.|

### TransferFromFailed
Event that is emitted when a Pantos cross-chain token
transfer failed on the source blockchain.


```solidity
event TransferFromFailed(
    uint256 sourceTransferId,
    PantosTypes.TransferFromRequest request,
    bytes signature,
    bytes32 sourceTokenData
);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sourceTransferId`|`uint256`|The unique Pantos transfer ID on the source blockchain.|
|`request`|`PantosTypes.TransferFromRequest`|The transfer request.|
|`signature`|`bytes`|The sender's signature.|
|`sourceTokenData`|`bytes32`|Optional PANDAS token data (may contain an error message).|

### TransferToSucceeded
Event that is emitted when a Pantos cross-chain token
transfer succeeded on the destination blockchain.


```solidity
event TransferToSucceeded(
    uint256 destinationTransferId,
    PantosTypes.TransferToRequest request,
    address[] signerAddresses,
    bytes[] signatures
);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`destinationTransferId`|`uint256`|The unique Pantos transfer ID on the destination blockchain.|
|`request`|`PantosTypes.TransferToRequest`|The transfer request.|
|`signerAddresses`|`address[]`|The addresses of the validator nodes that signed the transfer.|
|`signatures`|`bytes[]`|The signatures of the validator nodes (each signature is in the same array position as the corresponding signer address).|

## ABI

```json
[
  {
    "type": "function",
    "name": "cancelServiceNodeUnregistration",
    "inputs": [
      {
        "name": "serviceNodeAddress",
        "type": "address",
        "internalType": "address"
      }
    ],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "decreaseServiceNodeDeposit",
    "inputs": [
      {
        "name": "serviceNodeAddress",
        "type": "address",
        "internalType": "address"
      },
      {
        "name": "deposit",
        "type": "uint256",
        "internalType": "uint256"
      }
    ],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "executeMinimumServiceNodeDepositUpdate",
    "inputs": [],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "executeParameterUpdateDelayUpdate",
    "inputs": [],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "executeUnbondingPeriodServiceNodeDepositUpdate",
    "inputs": [],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "executeValidatorFeeFactorUpdate",
    "inputs": [
      {
        "name": "blockchainId",
        "type": "uint256",
        "internalType": "uint256"
      }
    ],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "getBlockchainRecord",
    "inputs": [
      {
        "name": "blockchainId",
        "type": "uint256",
        "internalType": "uint256"
      }
    ],
    "outputs": [
      {
        "name": "",
        "type": "tuple",
        "internalType": "struct PantosTypes.BlockchainRecord",
        "components": [
          {
            "name": "active",
            "type": "bool",
            "internalType": "bool"
          },
          {
            "name": "name",
            "type": "string",
            "internalType": "string"
          }
        ]
      }
    ],
    "stateMutability": "view"
  },
  {
    "type": "function",
    "name": "getCurrentBlockchainId",
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
    "name": "getCurrentMinimumServiceNodeDeposit",
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
    "name": "getCurrentParameterUpdateDelay",
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
    "name": "getCurrentUnbondingPeriodServiceNodeDeposit",
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
    "name": "getCurrentValidatorFeeFactor",
    "inputs": [
      {
        "name": "blockchainId",
        "type": "uint256",
        "internalType": "uint256"
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
    "name": "getExternalTokenRecord",
    "inputs": [
      {
        "name": "token",
        "type": "address",
        "internalType": "address"
      },
      {
        "name": "blockchainId",
        "type": "uint256",
        "internalType": "uint256"
      }
    ],
    "outputs": [
      {
        "name": "",
        "type": "tuple",
        "internalType": "struct PantosTypes.ExternalTokenRecord",
        "components": [
          {
            "name": "active",
            "type": "bool",
            "internalType": "bool"
          },
          {
            "name": "externalToken",
            "type": "string",
            "internalType": "string"
          }
        ]
      }
    ],
    "stateMutability": "view"
  },
  {
    "type": "function",
    "name": "getMinimumServiceNodeDeposit",
    "inputs": [],
    "outputs": [
      {
        "name": "",
        "type": "tuple",
        "internalType": "struct PantosTypes.UpdatableUint256",
        "components": [
          {
            "name": "currentValue",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "pendingValue",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "updateTime",
            "type": "uint256",
            "internalType": "uint256"
          }
        ]
      }
    ],
    "stateMutability": "view"
  },
  {
    "type": "function",
    "name": "getNextTransferId",
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
    "name": "getNumberActiveBlockchains",
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
    "name": "getNumberBlockchains",
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
    "name": "getPantosToken",
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
    "name": "getParameterUpdateDelay",
    "inputs": [],
    "outputs": [
      {
        "name": "",
        "type": "tuple",
        "internalType": "struct PantosTypes.UpdatableUint256",
        "components": [
          {
            "name": "currentValue",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "pendingValue",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "updateTime",
            "type": "uint256",
            "internalType": "uint256"
          }
        ]
      }
    ],
    "stateMutability": "view"
  },
  {
    "type": "function",
    "name": "getPrimaryValidatorNode",
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
    "name": "getServiceNodeRecord",
    "inputs": [
      {
        "name": "serviceNode",
        "type": "address",
        "internalType": "address"
      }
    ],
    "outputs": [
      {
        "name": "",
        "type": "tuple",
        "internalType": "struct PantosTypes.ServiceNodeRecord",
        "components": [
          {
            "name": "active",
            "type": "bool",
            "internalType": "bool"
          },
          {
            "name": "url",
            "type": "string",
            "internalType": "string"
          },
          {
            "name": "deposit",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "withdrawalAddress",
            "type": "address",
            "internalType": "address"
          },
          {
            "name": "withdrawalTime",
            "type": "uint256",
            "internalType": "uint256"
          }
        ]
      }
    ],
    "stateMutability": "view"
  },
  {
    "type": "function",
    "name": "getServiceNodes",
    "inputs": [],
    "outputs": [
      {
        "name": "",
        "type": "address[]",
        "internalType": "address[]"
      }
    ],
    "stateMutability": "view"
  },
  {
    "type": "function",
    "name": "getTokenRecord",
    "inputs": [
      {
        "name": "token",
        "type": "address",
        "internalType": "address"
      }
    ],
    "outputs": [
      {
        "name": "",
        "type": "tuple",
        "internalType": "struct PantosTypes.TokenRecord",
        "components": [
          {
            "name": "active",
            "type": "bool",
            "internalType": "bool"
          }
        ]
      }
    ],
    "stateMutability": "view"
  },
  {
    "type": "function",
    "name": "getTokens",
    "inputs": [],
    "outputs": [
      {
        "name": "",
        "type": "address[]",
        "internalType": "address[]"
      }
    ],
    "stateMutability": "view"
  },
  {
    "type": "function",
    "name": "getUnbondingPeriodServiceNodeDeposit",
    "inputs": [],
    "outputs": [
      {
        "name": "",
        "type": "tuple",
        "internalType": "struct PantosTypes.UpdatableUint256",
        "components": [
          {
            "name": "currentValue",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "pendingValue",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "updateTime",
            "type": "uint256",
            "internalType": "uint256"
          }
        ]
      }
    ],
    "stateMutability": "view"
  },
  {
    "type": "function",
    "name": "getValidatorFeeFactor",
    "inputs": [
      {
        "name": "blockchainId",
        "type": "uint256",
        "internalType": "uint256"
      }
    ],
    "outputs": [
      {
        "name": "",
        "type": "tuple",
        "internalType": "struct PantosTypes.UpdatableUint256",
        "components": [
          {
            "name": "currentValue",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "pendingValue",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "updateTime",
            "type": "uint256",
            "internalType": "uint256"
          }
        ]
      }
    ],
    "stateMutability": "view"
  },
  {
    "type": "function",
    "name": "increaseServiceNodeDeposit",
    "inputs": [
      {
        "name": "serviceNodeAddress",
        "type": "address",
        "internalType": "address"
      },
      {
        "name": "deposit",
        "type": "uint256",
        "internalType": "uint256"
      }
    ],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "initiateMinimumServiceNodeDepositUpdate",
    "inputs": [
      {
        "name": "newMinimumServiceNodeDeposit",
        "type": "uint256",
        "internalType": "uint256"
      }
    ],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "initiateParameterUpdateDelayUpdate",
    "inputs": [
      {
        "name": "newParameterUpdateDelay",
        "type": "uint256",
        "internalType": "uint256"
      }
    ],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "initiateUnbondingPeriodServiceNodeDepositUpdate",
    "inputs": [
      {
        "name": "newUnbondingPeriodServiceNodeDeposit",
        "type": "uint256",
        "internalType": "uint256"
      }
    ],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "initiateValidatorFeeFactorUpdate",
    "inputs": [
      {
        "name": "blockchainId",
        "type": "uint256",
        "internalType": "uint256"
      },
      {
        "name": "newValidatorFeeFactor",
        "type": "uint256",
        "internalType": "uint256"
      }
    ],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "isServiceNodeInTheUnbondingPeriod",
    "inputs": [
      {
        "name": "serviceNodeAddress",
        "type": "address",
        "internalType": "address"
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
    "name": "isValidSenderNonce",
    "inputs": [
      {
        "name": "sender",
        "type": "address",
        "internalType": "address"
      },
      {
        "name": "nonce",
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
    "stateMutability": "view"
  },
  {
    "type": "function",
    "name": "isValidValidatorNodeNonce",
    "inputs": [
      {
        "name": "nonce",
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
    "stateMutability": "view"
  },
  {
    "type": "function",
    "name": "pause",
    "inputs": [],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "paused",
    "inputs": [],
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
    "name": "registerBlockchain",
    "inputs": [
      {
        "name": "blockchainId",
        "type": "uint256",
        "internalType": "uint256"
      },
      {
        "name": "name",
        "type": "string",
        "internalType": "string"
      },
      {
        "name": "validatorFeeFactor",
        "type": "uint256",
        "internalType": "uint256"
      }
    ],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "registerExternalToken",
    "inputs": [
      {
        "name": "token",
        "type": "address",
        "internalType": "address"
      },
      {
        "name": "blockchainId",
        "type": "uint256",
        "internalType": "uint256"
      },
      {
        "name": "externalToken",
        "type": "string",
        "internalType": "string"
      }
    ],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "registerServiceNode",
    "inputs": [
      {
        "name": "serviceNodeAddress",
        "type": "address",
        "internalType": "address"
      },
      {
        "name": "url",
        "type": "string",
        "internalType": "string"
      },
      {
        "name": "deposit",
        "type": "uint256",
        "internalType": "uint256"
      },
      {
        "name": "withdrawalAddress",
        "type": "address",
        "internalType": "address"
      }
    ],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "registerToken",
    "inputs": [
      {
        "name": "token",
        "type": "address",
        "internalType": "address"
      }
    ],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "setPantosForwarder",
    "inputs": [
      {
        "name": "pantosForwarder",
        "type": "address",
        "internalType": "address"
      }
    ],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "setPantosToken",
    "inputs": [
      {
        "name": "pantosToken",
        "type": "address",
        "internalType": "address"
      }
    ],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "setPrimaryValidatorNode",
    "inputs": [
      {
        "name": "primaryValidatorNodeAddress",
        "type": "address",
        "internalType": "address"
      }
    ],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "transfer",
    "inputs": [
      {
        "name": "request",
        "type": "tuple",
        "internalType": "struct PantosTypes.TransferRequest",
        "components": [
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
            "name": "token",
            "type": "address",
            "internalType": "address"
          },
          {
            "name": "amount",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "serviceNode",
            "type": "address",
            "internalType": "address"
          },
          {
            "name": "fee",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "nonce",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "validUntil",
            "type": "uint256",
            "internalType": "uint256"
          }
        ]
      },
      {
        "name": "signature",
        "type": "bytes",
        "internalType": "bytes"
      }
    ],
    "outputs": [
      {
        "name": "",
        "type": "uint256",
        "internalType": "uint256"
      }
    ],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "transferFrom",
    "inputs": [
      {
        "name": "request",
        "type": "tuple",
        "internalType": "struct PantosTypes.TransferFromRequest",
        "components": [
          {
            "name": "destinationBlockchainId",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "sender",
            "type": "address",
            "internalType": "address"
          },
          {
            "name": "recipient",
            "type": "string",
            "internalType": "string"
          },
          {
            "name": "sourceToken",
            "type": "address",
            "internalType": "address"
          },
          {
            "name": "destinationToken",
            "type": "string",
            "internalType": "string"
          },
          {
            "name": "amount",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "serviceNode",
            "type": "address",
            "internalType": "address"
          },
          {
            "name": "fee",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "nonce",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "validUntil",
            "type": "uint256",
            "internalType": "uint256"
          }
        ]
      },
      {
        "name": "signature",
        "type": "bytes",
        "internalType": "bytes"
      }
    ],
    "outputs": [
      {
        "name": "",
        "type": "uint256",
        "internalType": "uint256"
      }
    ],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "transferTo",
    "inputs": [
      {
        "name": "request",
        "type": "tuple",
        "internalType": "struct PantosTypes.TransferToRequest",
        "components": [
          {
            "name": "sourceBlockchainId",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "sourceTransferId",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "sourceTransactionId",
            "type": "string",
            "internalType": "string"
          },
          {
            "name": "sender",
            "type": "string",
            "internalType": "string"
          },
          {
            "name": "recipient",
            "type": "address",
            "internalType": "address"
          },
          {
            "name": "sourceToken",
            "type": "string",
            "internalType": "string"
          },
          {
            "name": "destinationToken",
            "type": "address",
            "internalType": "address"
          },
          {
            "name": "amount",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "nonce",
            "type": "uint256",
            "internalType": "uint256"
          }
        ]
      },
      {
        "name": "signerAddresses",
        "type": "address[]",
        "internalType": "address[]"
      },
      {
        "name": "signatures",
        "type": "bytes[]",
        "internalType": "bytes[]"
      }
    ],
    "outputs": [
      {
        "name": "",
        "type": "uint256",
        "internalType": "uint256"
      }
    ],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "unpause",
    "inputs": [],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "unregisterBlockchain",
    "inputs": [
      {
        "name": "blockchainId",
        "type": "uint256",
        "internalType": "uint256"
      }
    ],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "unregisterExternalToken",
    "inputs": [
      {
        "name": "token",
        "type": "address",
        "internalType": "address"
      },
      {
        "name": "blockchainId",
        "type": "uint256",
        "internalType": "uint256"
      }
    ],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "unregisterServiceNode",
    "inputs": [
      {
        "name": "serviceNodeAddress",
        "type": "address",
        "internalType": "address"
      }
    ],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "unregisterToken",
    "inputs": [
      {
        "name": "token",
        "type": "address",
        "internalType": "address"
      }
    ],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "updateBlockchainName",
    "inputs": [
      {
        "name": "blockchainId",
        "type": "uint256",
        "internalType": "uint256"
      },
      {
        "name": "name",
        "type": "string",
        "internalType": "string"
      }
    ],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "updateServiceNodeUrl",
    "inputs": [
      {
        "name": "url",
        "type": "string",
        "internalType": "string"
      }
    ],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "function",
    "name": "verifyTransfer",
    "inputs": [
      {
        "name": "request",
        "type": "tuple",
        "internalType": "struct PantosTypes.TransferRequest",
        "components": [
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
            "name": "token",
            "type": "address",
            "internalType": "address"
          },
          {
            "name": "amount",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "serviceNode",
            "type": "address",
            "internalType": "address"
          },
          {
            "name": "fee",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "nonce",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "validUntil",
            "type": "uint256",
            "internalType": "uint256"
          }
        ]
      },
      {
        "name": "signature",
        "type": "bytes",
        "internalType": "bytes"
      }
    ],
    "outputs": [],
    "stateMutability": "view"
  },
  {
    "type": "function",
    "name": "verifyTransferFrom",
    "inputs": [
      {
        "name": "request",
        "type": "tuple",
        "internalType": "struct PantosTypes.TransferFromRequest",
        "components": [
          {
            "name": "destinationBlockchainId",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "sender",
            "type": "address",
            "internalType": "address"
          },
          {
            "name": "recipient",
            "type": "string",
            "internalType": "string"
          },
          {
            "name": "sourceToken",
            "type": "address",
            "internalType": "address"
          },
          {
            "name": "destinationToken",
            "type": "string",
            "internalType": "string"
          },
          {
            "name": "amount",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "serviceNode",
            "type": "address",
            "internalType": "address"
          },
          {
            "name": "fee",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "nonce",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "validUntil",
            "type": "uint256",
            "internalType": "uint256"
          }
        ]
      },
      {
        "name": "signature",
        "type": "bytes",
        "internalType": "bytes"
      }
    ],
    "outputs": [],
    "stateMutability": "view"
  },
  {
    "type": "function",
    "name": "verifyTransferTo",
    "inputs": [
      {
        "name": "request",
        "type": "tuple",
        "internalType": "struct PantosTypes.TransferToRequest",
        "components": [
          {
            "name": "sourceBlockchainId",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "sourceTransferId",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "sourceTransactionId",
            "type": "string",
            "internalType": "string"
          },
          {
            "name": "sender",
            "type": "string",
            "internalType": "string"
          },
          {
            "name": "recipient",
            "type": "address",
            "internalType": "address"
          },
          {
            "name": "sourceToken",
            "type": "string",
            "internalType": "string"
          },
          {
            "name": "destinationToken",
            "type": "address",
            "internalType": "address"
          },
          {
            "name": "amount",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "nonce",
            "type": "uint256",
            "internalType": "uint256"
          }
        ]
      },
      {
        "name": "signerAddresses",
        "type": "address[]",
        "internalType": "address[]"
      },
      {
        "name": "signatures",
        "type": "bytes[]",
        "internalType": "bytes[]"
      }
    ],
    "outputs": [],
    "stateMutability": "view"
  },
  {
    "type": "function",
    "name": "withdrawServiceNodeDeposit",
    "inputs": [
      {
        "name": "serviceNodeAddress",
        "type": "address",
        "internalType": "address"
      }
    ],
    "outputs": [],
    "stateMutability": "nonpayable"
  },
  {
    "type": "event",
    "name": "BlockchainNameUpdated",
    "inputs": [
      {
        "name": "blockchainId",
        "type": "uint256",
        "indexed": false,
        "internalType": "uint256"
      }
    ],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "BlockchainRegistered",
    "inputs": [
      {
        "name": "blockchainId",
        "type": "uint256",
        "indexed": false,
        "internalType": "uint256"
      },
      {
        "name": "validatorFeeFactor",
        "type": "uint256",
        "indexed": false,
        "internalType": "uint256"
      }
    ],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "BlockchainUnregistered",
    "inputs": [
      {
        "name": "blockchainId",
        "type": "uint256",
        "indexed": false,
        "internalType": "uint256"
      }
    ],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "ExternalTokenRegistered",
    "inputs": [
      {
        "name": "token",
        "type": "address",
        "indexed": false,
        "internalType": "address"
      },
      {
        "name": "blockchainId",
        "type": "uint256",
        "indexed": false,
        "internalType": "uint256"
      }
    ],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "ExternalTokenUnregistered",
    "inputs": [
      {
        "name": "token",
        "type": "address",
        "indexed": false,
        "internalType": "address"
      },
      {
        "name": "blockchainId",
        "type": "uint256",
        "indexed": false,
        "internalType": "uint256"
      }
    ],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "MinimumServiceNodeDepositUpdateExecuted",
    "inputs": [
      {
        "name": "newMinimumServiceNodeDeposit",
        "type": "uint256",
        "indexed": false,
        "internalType": "uint256"
      }
    ],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "MinimumServiceNodeDepositUpdateInitiated",
    "inputs": [
      {
        "name": "newMinimumServiceNodeDeposit",
        "type": "uint256",
        "indexed": false,
        "internalType": "uint256"
      },
      {
        "name": "earliestUpdateTime",
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
    "name": "PantosTokenSet",
    "inputs": [
      {
        "name": "pantosToken",
        "type": "address",
        "indexed": false,
        "internalType": "address"
      }
    ],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "ParameterUpdateDelayUpdateExecuted",
    "inputs": [
      {
        "name": "newParameterUpdateDelay",
        "type": "uint256",
        "indexed": false,
        "internalType": "uint256"
      }
    ],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "ParameterUpdateDelayUpdateInitiated",
    "inputs": [
      {
        "name": "newParameterUpdateDelay",
        "type": "uint256",
        "indexed": false,
        "internalType": "uint256"
      },
      {
        "name": "earliestUpdateTime",
        "type": "uint256",
        "indexed": false,
        "internalType": "uint256"
      }
    ],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "Paused",
    "inputs": [
      {
        "name": "account",
        "type": "address",
        "indexed": false,
        "internalType": "address"
      }
    ],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "PrimaryValidatorNodeUpdated",
    "inputs": [
      {
        "name": "primaryValidatorNodeAddress",
        "type": "address",
        "indexed": false,
        "internalType": "address"
      }
    ],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "ServiceNodeRegistered",
    "inputs": [
      {
        "name": "serviceNode",
        "type": "address",
        "indexed": false,
        "internalType": "address"
      }
    ],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "ServiceNodeUnregistered",
    "inputs": [
      {
        "name": "serviceNode",
        "type": "address",
        "indexed": false,
        "internalType": "address"
      }
    ],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "ServiceNodeUrlUpdated",
    "inputs": [
      {
        "name": "serviceNode",
        "type": "address",
        "indexed": false,
        "internalType": "address"
      }
    ],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "TokenRegistered",
    "inputs": [
      {
        "name": "token",
        "type": "address",
        "indexed": false,
        "internalType": "address"
      }
    ],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "TokenUnregistered",
    "inputs": [
      {
        "name": "token",
        "type": "address",
        "indexed": false,
        "internalType": "address"
      }
    ],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "TransferFailed",
    "inputs": [
      {
        "name": "transferId",
        "type": "uint256",
        "indexed": false,
        "internalType": "uint256"
      },
      {
        "name": "request",
        "type": "tuple",
        "indexed": false,
        "internalType": "struct PantosTypes.TransferRequest",
        "components": [
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
            "name": "token",
            "type": "address",
            "internalType": "address"
          },
          {
            "name": "amount",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "serviceNode",
            "type": "address",
            "internalType": "address"
          },
          {
            "name": "fee",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "nonce",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "validUntil",
            "type": "uint256",
            "internalType": "uint256"
          }
        ]
      },
      {
        "name": "signature",
        "type": "bytes",
        "indexed": false,
        "internalType": "bytes"
      },
      {
        "name": "tokenData",
        "type": "bytes32",
        "indexed": false,
        "internalType": "bytes32"
      }
    ],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "TransferFromFailed",
    "inputs": [
      {
        "name": "sourceTransferId",
        "type": "uint256",
        "indexed": false,
        "internalType": "uint256"
      },
      {
        "name": "request",
        "type": "tuple",
        "indexed": false,
        "internalType": "struct PantosTypes.TransferFromRequest",
        "components": [
          {
            "name": "destinationBlockchainId",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "sender",
            "type": "address",
            "internalType": "address"
          },
          {
            "name": "recipient",
            "type": "string",
            "internalType": "string"
          },
          {
            "name": "sourceToken",
            "type": "address",
            "internalType": "address"
          },
          {
            "name": "destinationToken",
            "type": "string",
            "internalType": "string"
          },
          {
            "name": "amount",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "serviceNode",
            "type": "address",
            "internalType": "address"
          },
          {
            "name": "fee",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "nonce",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "validUntil",
            "type": "uint256",
            "internalType": "uint256"
          }
        ]
      },
      {
        "name": "signature",
        "type": "bytes",
        "indexed": false,
        "internalType": "bytes"
      },
      {
        "name": "sourceTokenData",
        "type": "bytes32",
        "indexed": false,
        "internalType": "bytes32"
      }
    ],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "TransferFromSucceeded",
    "inputs": [
      {
        "name": "sourceTransferId",
        "type": "uint256",
        "indexed": false,
        "internalType": "uint256"
      },
      {
        "name": "request",
        "type": "tuple",
        "indexed": false,
        "internalType": "struct PantosTypes.TransferFromRequest",
        "components": [
          {
            "name": "destinationBlockchainId",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "sender",
            "type": "address",
            "internalType": "address"
          },
          {
            "name": "recipient",
            "type": "string",
            "internalType": "string"
          },
          {
            "name": "sourceToken",
            "type": "address",
            "internalType": "address"
          },
          {
            "name": "destinationToken",
            "type": "string",
            "internalType": "string"
          },
          {
            "name": "amount",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "serviceNode",
            "type": "address",
            "internalType": "address"
          },
          {
            "name": "fee",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "nonce",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "validUntil",
            "type": "uint256",
            "internalType": "uint256"
          }
        ]
      },
      {
        "name": "signature",
        "type": "bytes",
        "indexed": false,
        "internalType": "bytes"
      }
    ],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "TransferSucceeded",
    "inputs": [
      {
        "name": "transferId",
        "type": "uint256",
        "indexed": false,
        "internalType": "uint256"
      },
      {
        "name": "request",
        "type": "tuple",
        "indexed": false,
        "internalType": "struct PantosTypes.TransferRequest",
        "components": [
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
            "name": "token",
            "type": "address",
            "internalType": "address"
          },
          {
            "name": "amount",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "serviceNode",
            "type": "address",
            "internalType": "address"
          },
          {
            "name": "fee",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "nonce",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "validUntil",
            "type": "uint256",
            "internalType": "uint256"
          }
        ]
      },
      {
        "name": "signature",
        "type": "bytes",
        "indexed": false,
        "internalType": "bytes"
      }
    ],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "TransferToSucceeded",
    "inputs": [
      {
        "name": "destinationTransferId",
        "type": "uint256",
        "indexed": false,
        "internalType": "uint256"
      },
      {
        "name": "request",
        "type": "tuple",
        "indexed": false,
        "internalType": "struct PantosTypes.TransferToRequest",
        "components": [
          {
            "name": "sourceBlockchainId",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "sourceTransferId",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "sourceTransactionId",
            "type": "string",
            "internalType": "string"
          },
          {
            "name": "sender",
            "type": "string",
            "internalType": "string"
          },
          {
            "name": "recipient",
            "type": "address",
            "internalType": "address"
          },
          {
            "name": "sourceToken",
            "type": "string",
            "internalType": "string"
          },
          {
            "name": "destinationToken",
            "type": "address",
            "internalType": "address"
          },
          {
            "name": "amount",
            "type": "uint256",
            "internalType": "uint256"
          },
          {
            "name": "nonce",
            "type": "uint256",
            "internalType": "uint256"
          }
        ]
      },
      {
        "name": "signerAddresses",
        "type": "address[]",
        "indexed": false,
        "internalType": "address[]"
      },
      {
        "name": "signatures",
        "type": "bytes[]",
        "indexed": false,
        "internalType": "bytes[]"
      }
    ],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "UnbondingPeriodServiceNodeDepositUpdateExecuted",
    "inputs": [
      {
        "name": "newUnbondingPeriodServiceNodeDeposit",
        "type": "uint256",
        "indexed": false,
        "internalType": "uint256"
      }
    ],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "UnbondingPeriodServiceNodeDepositUpdateInitiated",
    "inputs": [
      {
        "name": "newUnbondingPeriodServiceNodeDeposit",
        "type": "uint256",
        "indexed": false,
        "internalType": "uint256"
      },
      {
        "name": "earliestUpdateTime",
        "type": "uint256",
        "indexed": false,
        "internalType": "uint256"
      }
    ],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "Unpaused",
    "inputs": [
      {
        "name": "account",
        "type": "address",
        "indexed": false,
        "internalType": "address"
      }
    ],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "ValidatorFeeFactorUpdateExecuted",
    "inputs": [
      {
        "name": "blockchainId",
        "type": "uint256",
        "indexed": false,
        "internalType": "uint256"
      },
      {
        "name": "newValidatorFeeFactor",
        "type": "uint256",
        "indexed": false,
        "internalType": "uint256"
      }
    ],
    "anonymous": false
  },
  {
    "type": "event",
    "name": "ValidatorFeeFactorUpdateInitiated",
    "inputs": [
      {
        "name": "blockchainId",
        "type": "uint256",
        "indexed": false,
        "internalType": "uint256"
      },
      {
        "name": "newValidatorFeeFactor",
        "type": "uint256",
        "indexed": false,
        "internalType": "uint256"
      },
      {
        "name": "earliestUpdateTime",
        "type": "uint256",
        "indexed": false,
        "internalType": "uint256"
      }
    ],
    "anonymous": false
  }
]
```
