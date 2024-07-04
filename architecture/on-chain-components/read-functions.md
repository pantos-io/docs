# Read functions

The contracts provide several read functions, which do not require a transaction being sent to the blockchain. Here is a list of those functions:

### Pantos Forwarder <a href="#pantos-forwarder" id="pantos-forwarder"></a>

* **getPantosHub()**: Returns the address of the Pantos Hub contract
* **getPantosToken()**: Returns the address of the Pantos Token contract
* **getPantosValidator()**: Returns the address of the Trusted Validator

### Pantos Base Token <a href="#pantos-base-token" id="pantos-base-token"></a>

* **decimals()**: Returns the number of decimals the token has
* **symbol()**: Returns the symbol of the token (e.g. PAN)
* **name()**: Returns the name of the token (e.g. Pantos)
* **getOwner()**: Returns the address of the owner of the Token address
* **getPantosForwarder()**: Returns the address of the Pantos Forwarder contract

### Pantos Hub <a href="#pantos-hub" id="pantos-hub"></a>

* **getPantosForwarder()**: Returns the address of the Pantos Forwarder contract
* **getPantosToken()**: Returns the address of the Pantos Token contract
* **getPantosValidator()**: Returns the address of the Trusted Validator
* **getNumberBlockchains()**: Returns the total number of blockchains, registered and deregistered
* **getNumberActiveBlockchains()**: Returns the number of active blockchains registered
* **getCurrentBlockchainId()**: Returns the id of the blockchain the Pantos Hub contract resides on
* **getBlockchainRecord(uint256 chainID)**: Returns a blockchain record struct for the given blockchain id
* **getMinimumTokenStake()**: Returns the current minimum number of Pantos tokens required to register a token in the Pantos Hub contract
* **getMinimumServiceNodeStake()**: Returns the current minimum number of Pantos tokens required in order to register as a service node
* **getTokens()**: Returns a list of all active tokens registered at the Pantos Hub contract
* **getTokenRecord(address token)**: Returns a token record for a given token address
* **getExternalTokenRecord(address token, uint256 chainID)**: Returns an external token record for a token which resides on a blockchain with a blockchain id different from the current blockchain id
* **getServiceNodes()**: Returns a list of active service nodes
* **getServiceNodeRecord(address serviceNode)**: Returns a service node record for a service node with address serviceNode
* **getServiceNodeBidRecord(address serviceNode, uint256 bidID)**: Returns a bid record for a service node with address serviceNode and id bidID
