---
description: >-
  This guide will assist you in migrating your PANDAS token contract from the
  old Pantos Hub contract to a new version.
---

# Migrate Token

This documentation provides a comprehensive guide to migrating your PANDAS token contract from the old Pantos Hub contract to its newer version. Periodic migrations might be necessary due to updates or enhancements in the Pantos Hub contract.

### Requirements

1. **Ownership**: You must possess the private key of the owner of the PANDAS token contract.
2. **Functionality**: The PANDAS token contract should include the `setForwarder` function.
3. **Contract Addresses**: Keep handy the addresses of the new Pantos Hub and Forwarder contract. [testnet-addresses.md](testnet-addresses.md "mention")

## **Migration Steps**

1. **Unregistration**: Initiate the migration by invoking the `unregisterToken` function. Provide the address of your token as the function parameter.
   * This step will deregister your token, any linked external tokens, and subsequently return your PAN stake.
2. **Stake Approval**: Approve the requisite Pantos stake amount for the new Pantos Hub contract.
3. **Token Registration**: Register your token to the new Pantos Hub. Use the `registerToken` function for this operation.
4. **External Token Registration**: Ensure you register all linked external tokens to the new Pantos Hub.
5. **Set new Pantos Forwarder**: Use the \`setForwarder\` function of your Pandas Token contract in order to update the Pantos Forwarder address

### **Automation Script**

For those familiar with Brownie, we provide an automated script to streamline the migration process:

```python
import brownie
import enum
import json

PRIORITY_FEE = '3 gwei'

class Blockchain(enum.IntEnum):
    """Enumeration of supported blockchain networks.

    """
    ETHEREUM = 0
    BNB_CHAIN = 1
    AVALANCHE = 3
    SOLANA = 4
    POLYGON = 5
    CRONOS = 6
    FANTOM = 7
    CELO = 8

    @staticmethod
    def from_name(name: str) -> 'Blockchain':
        """Find an enumeration member by its name.

        Parameters
        ----------
        name : str
            The name to search for.

        Raises
        ------
        NameError
            If no enumeration member can be found for the given name.

        """
        name_upper = name.upper()
        for blockchain in Blockchain:
            if name_upper == blockchain.name:
                return blockchain
        raise NameError(name)


def get_external_tokens(pantos_hub, pandas_token_address):
    registered_external_tokens = {}
    for blockchain in Blockchain:
        try:
            external_token_record = pantos_hub.getExternalTokenRecord(
                pandas_token_address, blockchain.value)
        except ValueError as error:
            raw_record_data = str(error).split(' - ')[0]
            if 'True' in raw_record_data:
                external_token_record = (
                    True, raw_record_data.split('True, \'')[1].split('\')')[0])
        if external_token_record[0]:
            registered_external_tokens[blockchain] = external_token_record[1]

    return registered_external_tokens


def main(account_name: str, old_pantos_hub_address: str,
         forwarder_address: str, new_pantos_hub_address: str,
         your_token_address: str, pantos_token_address: str) -> None:
    brownie.network.gas_price('auto')
    brownie.network.priority_fee(PRIORITY_FEE)
    account = brownie.accounts.load(account_name)
    transaction_parameters = {'from': account}

    with open('./path/to/pantos_hub_abi.json', 'r') as f:
        pantos_hub_abi_data = json.loads(f.read())

    # loading Pantos Token abi data
    with open('./path/to/pantos_token_abi.json', 'r') as f:
        pantos_token_abi_data = json.loads(f.read())

    old_hub = brownie.Contract.from_abi("PantosHub", old_pantos_hub_address,
                                        pantos_hub_abi_data['abi'])
    new_hub = brownie.Contract.from_abi("PantosHub", new_pantos_hub_address,
                                        pantos_hub_abi_data['abi'])

    my_pandas_token = brownie.Contract.from_abi("PantosToken",
                                                your_token_address,
                                                pantos_token_abi_data['abi'])
    pantos_token = brownie.Contract.from_abi("PantosToken",
                                             pantos_token_address,
                                             pantos_token_abi_data['abi'])

    external_tokens = get_external_tokens(old_hub, your_token_address)

    old_hub.unregisterToken(my_pandas_token.address, transaction_parameters)

    pantos_token.approve(new_hub.address, _MINIMUM_TOKEN_STAKE,
                         transaction_parameters)

    new_hub.registerToken(my_pandas_token.address, _MINIMUM_TOKEN_STAKE,
                          transaction_parameters)

    for external_token in external_tokens:
        try:
            record = new_hub.getExternalTokenRecord(my_pandas_token.address,
                                                    external_token.value)
        except ValueError as error:
            record = [True] if ('True' in str(error)) else [False]
        if not record[0]:
            new_hub.registerExternalToken(
                my_pandas_token.address, external_token.value,
                external_tokens[external_token].encode('utf-8').strip(),
                transaction_parameters)

    my_pandas_token.setPantosForwarder(forwarder_address,
                                       transaction_parameters)
```
