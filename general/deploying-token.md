---
description: In this example we show how to deploy a PANDAS-based Token using Brownie
---

# Deploying Token

## Prerequisites

* Install Brownie: pip install eth-brownie
* Add your custom token contract to the contracts folder in your Brownie project.
* Add your private key to the brownie project
  * If you have already a private key, use: `brownie accounts new <id>`
  * If you don't have a private key, use: `brownie accounts generate <id>`
    * Do not forget to request testnet funds from the faucets
* Modify the networks-config.yaml to include the desired testnets.

#### Step 1: Configure the networks-config.yaml

Update the networks-config.yaml file to include the testnet configurations for Ethereum (Goerli), BNB Chain (Testnet), Avalanche (Fuji), Fantom (Testnet), Celo (Alfajores), and Cronos (Testnet).

```
networks:
- name: Goerli
  networks:
    - name: Testnet
      chainid: 5
      id: goerli-test
      host: https://goerli.infura.io/v3/YOUR-PROJECT-ID
      explorer: https://goerli.etherscan.io/api

- name: BNB Chain
  networks:
    - name: Testnet
      chainid: 97
      id: bnb-test
      host: https://data-seed-prebsc-1-s1.binance.org:8545
      explorer: https://testnet.bscscan.com/api

- name: Avalanche
  networks:
    - name: Testnet
      chainid: 43113
      id: avalanche-fuji
      host: https://api.avax-test.network/ext/bc/C/rpc
      explorer: https://cchain.explorer.avax-test.network/api

- name: Fantom
  networks:
    - name: Testnet
      chainid: 4002
      id: fantom-test
      host: https://rpc.testnet.fantom.network
      explorer: https://explorer.testnet.fantom.network/api

- name: Celo
  networks:
    - name: Testnet
      chainid: 44787
      id: celo-alfajores
      host: https://alfajores-forno.celo-testnet.org
      explorer: https://alfajores-blockscout.celo-testnet.org/api

- name: Cronos
  networks:
    - name: Testnet
      chainid: 338
      id: cronos-test
      host: https://evm-t3.cronos.org/
      explorer: https://cronos-explorer.crypto.org/api

```

#### Step 2: Add OpenZeppelin dependencies to brownie-config.yaml

Add the following lines to your brownie-config.yaml file in order to be able to download the OpenZeppelin dependencies:

```yaml
compiler:
    solc:
        version: 0.8.17
        remappings:
            - "@openzeppelin=OpenZeppelin/openzeppelin-contracts@4.1.0"
            - "@openzeppelin-upgradeable=OpenZeppelin/openzeppelin-contracts-upgradeable@4.8.1"

dependencies:
  - OpenZeppelin/openzeppelin-contracts@4.1.0
  - OpenZeppelin/openzeppelin-contracts-upgradeable@4.8.1
```

#### Step 3: Deploy and register your token on each supported testnet

In your Brownie project, create a scripts directory and add a file named deploy\_token.py and add the following code:&#x20;

```python
import brownie
import json

from brownie import MyToken

# Set initial token supply and minimum token stake
INITIAL_SUPPLY = 100 * 10**18 # initial supply is 100 Token with 18 decimals
_MINIMUM_TOKEN_STAKE = 1

# Set the addresses for the Pantos forwarder, hub, and PAN token
FORWARDER_ADDRESS = "get address bottom of this page"
HUB_ADDRESS = "get address bottom of this page"
PAN_ADDRESS = "get address bottom of this page"

# Define the deployToken function
def deploy_token(account_name: str):
        # loading Pantos Hub abi data
        with open('./path/to/pantos_hub_abi.json', 'r') as f:
            pantos_hub_abi_data = json.loads(f.read())

        # loading Pantos Token abi data
	with open('./path/to/pantos_token_abi.json', 'r') as f:
            pantos_token_abi_data = json.loads(f.read())
            
	# Load the PantosHub contract from the ABI
	hub = brownie.Contract.from_abi("PantosHub", HUB_ADDRESS,
	                                pantos_hub_abi_data['abi'])
    
	# Load the PantosToken contract from the ABI
	pan_token = brownie.Contract.from_abi("PantosToken", PAN_ADDRESS,
                                      	      pantos_token_abi_data['abi'])

	# Load the specified account
	account = brownie.accounts.load(account_name)

	# Deploy the custom token contract
	myTokenContract = MyToken.deploy(INITIAL_SUPPLY, {'from': account})

	# Set the Pantos forwarder address in the custom token contract
	myTokenContract.setPantosForwarder(FORWARDER_ADDRESS,
                                   	   {'from': account})

	# Approve the PantosHub to spend the required minimum token stake
	pan_token.approve(HUB_ADDRESS, _MINIMUM_TOKEN_STAKE, {'from': account})

	# Register the custom token on the PantosHub
	hub.registerToken(myTokenContract.address, _MINIMUM_TOKEN_STAKE,
                  	{'from': account})
```

Set the **FORWARDER\_ADDRESS, HUB\_ADDRESS & PAN\_ADDRESS** with the appropriate addresses for each testnet.&#x20;

Run the script on each testnet using Brownie:

```bash
brownie run ./scripts/deploy_token.py deploy_token <name of account> --network <network name>
```

#### Step 4: Register external tokens on each Pantos Hub

**registerExternalToken** is a function used in the Pantos ecosystem to establish a connection between a token on one blockchain and its corresponding token on another blockchain. This function enables the PantosHub to recognize the token's presence across multiple blockchains and helps facilitate cross-chain token transfers.

Create a file named **register\_external\_tokens.py** in the scripts directory of your Brownie project and add the following code:

<pre class="language-python"><code class="lang-python">import brownie


<strong>def register_token(account_name: str):
</strong>        with open('./path/to/pantos_hub_abi.json', 'r') as f:
            pantos_hub_abi_data = json.loads(f.read())
	# Load the PantosHub contract from the ABI
	hub = brownie.Contract.from_abi("PantosHub", HUB_ADDRESS,
	                                pantos_hub_abi_data['abi'])
    
	# Load the specified account
	account = brownie.accounts.load(account_name)

	# Call the registerExternalToken function from the PantosHub contract
	# Replace the placeholders with the correct data:
	# - &#x3C;address of token on chain>: the address of your token on the current chain
	# - &#x3C;chain id>: the ID of the blockchain where the external token is located
	# - &#x3C;address of token on different chain>: the address of your token on the external chain
	hub.registerExternalToken(
    	  &#x3C;address of token on chain>,
    	  &#x3C;chain id>,
    	  &#x3C;address of token on different chain>.encode('utf-8').strip(),
    	  {'from': account}
	)
</code></pre>

Replace **\<address of token on chain>, \<chain id> & \<address of token on different chain>** with the appropriate addresses for each testnet.&#x20;

Run the script on each testnet using Brownie:

```
brownie run ./scripts/register_external_tokens.py register_token <name of account> --network <network name>
```

Once you have completed these steps, your token will be deployed on all the supported testnets and registered with the Pantos Hubs. This will enable your token to be transferred across these networks seamlessly.

To summarize, this step-by-step guide will help you deploy your token on multiple testnets and register it with the Pantos Hubs. You will need to create a Brownie project, configure the necessary networks, deploy your token, and run the appropriate scripts to register your token and external tokens on each Pantos Hub. By following these steps, you'll have a multichain token that can be used across different blockchain networks.

Feel free to add your registered tokens to this list: [https://github.com/pantos-io/testnet-token-list](https://github.com/pantos-io/testnet-token-list)

#### Overview of Pantos Blockchain IDs & Contract Addresses

All addresses and ids can be found here: [testnet-addresses.md](testnet-addresses.md "mention")

{% hint style="info" %}
Use Pantos Chain ID for Pantos transactions only like "registerExternalToken". For contract deployment, use standard EVM Chain IDs.
{% endhint %}
