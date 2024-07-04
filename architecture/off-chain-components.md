# Off-Chain Components

## Trusted Validator

The Trusted Validator in the current stage is the one who performs the second step of a cross-chain transfer by minting the transferred tokens in the users account. In order to mint those tokens, it listens to events on the PantosHub contracts accross the [supported-chains.md](../general/supported-chains.md "mention") and once it hears an event initiating a cross-chain transfer, it mints the tokens on the destination chain.

In the current stage of Pantos, it is operated by Pantos and will be decentralized at a later point in time, allowing users to operate a Trusted Validator.

## Service Node

The Service Node is the first decentralised component in Pantos and can be operated by any user. It registers itself in the PantosHub contracts on the blockchains it wants to operate on and offers users a list of supported cross-blockchain transfers + fees. It accepts signed request for a cross-blockchain transfer and initiates the cross-chain transfer by burning the tokens on the source chain in the users account.

## Faucet

A cryptocurrency "faucet" is a site that gives away coins and tokens. Faucets are common on test networks such as Ethereum's Goerli, Polygon's Mumbai, and more. It allows developers to test their applications with tokens which have no monetary value. \
Pantos also offers a faucet, which allows users to obtain Pantos tokens in order to be able to try out the Pantos protocol on the [supported-chains.md](../general/supported-chains.md "mention").
