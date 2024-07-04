# On-Chain Components

## Pantos Hub

This is the core on-chain component of Pantos. The Pantos Hub contract is available on each of the supported blockchains. It is an interface for off-chain components and as the name implies it is the main contract for node & client requests. The contract handles the registration of new tokens and the management. Additionally, it also handles the registration and management of service nodes, as well as the corresponding service node bids.

## Pantos Forwarder

Responsible for verifying transfer requests and signatures, to ensure the validity of a transfer before initiating a transaction. The Pantos forwarder contract connects the Pantos Hub to the token contract and initiates on-chain transactions for burn and mint.

## Pantos Tokens&#x20;

As last on-chain component the Pantos tokens,&#x20;

* Fully compatible with existing token standards
* e.g. ERC-20 on Ethereum
* Additional simple Pantos-specific interface
* Anyone can deploy Pantos-compatible tokens
* Permissionless
* May support all or subset of blockchains
* Need to be registered at the Pantos hub
* Transaction fees always paid in PAN





<figure><img src="https://lh4.googleusercontent.com/ZAjrykYXTst-Dny5iS80EcJhlDKJEEObON9enhLF5-nmRaUGNeruQa0jk4KsKh4WrC9tkau53hf14UDwnH8GkkAYJFxcP3k9n-Bz1aP3N4ZUDh5IbCZMqUfQjiy7qDq5W0U06B5KLwcxWQmaXsd7uGsSFzkK7CefnZHVso1U79KfJ4MZQGMLtM1I4NFN-z4L" alt=""><figcaption><p>Chain A (yellow) -> Chain B (green)</p></figcaption></figure>
