# Service Node

## Setting up a Pantos Service Node

### Prerequisites

**Minimum hardware requirements for a Pantos Service Node instance:**

> CPU: At least a single-core CPU

> Memory (RAM): A minimum of 2 GB of RAM

> Storage: At least 8 GB of available storage space

Please note that these are the minimum hardware requirements, and actual hardware needs may vary depending on the specific workload and usage patterns of the service node. It's recommended to provide additional resources if the software will be handling a constant high volume of data. To install and run your own Pantos Service Node instance, you need a server (e.g. a virtual private server hosted by an Internet service provider) running a current GNU/Linux distribution.

The easiest way to get started and set up your Service Node is by using a Debian or Ubuntu server. We recommend either Debian Stable (currently Debian 12) or Ubuntu LTS (currently Ubuntu 22.04 LTS). More experienced users can also use other GNU/Linux distributions to set up their Service Node instance.

For this guide, we assume that you are familiar with GNU/Linux in general (including the most important shell commands) and you have (at least) basic system administration and networking skills. In the first section of this guide, we cover the recommended installation of a Pantos Service Node instance using the package manager of Debian/Ubuntu. In the second section, we describe how to install your Service Node instance manually on Debian/Ubuntu. Advanced users may adapt these steps to set up a Service Node instance on other GNU/Linux distributions (or even other operating systems).

## Step 1 - Installation Steps

**Download and install the Pantos Service Node package:**

```
curl -s --compressed "https://pantos-io.github.io/servicenode/KEY.gpg" | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/servicenode.gpg >/dev/null
sudo curl -s --compressed -o /etc/apt/sources.list.d/pantos-servicenode.list "https://pantos-io.github.io/servicenode/pantos-servicenode.list"
sudo apt update
sudo apt install pantos-service-node
```

This will install the Service Node and its dependencies, including Apache, PostgreSQL, and RabbitMQ.

It will also set up the required users, directories, access rights, databases, and message broker host. The Service Node is not started automatically since you have to perform a few configuration steps manually first.

## Step 2: Generating an SSL Certificate for the Domain

### Install Certbot

**Install Certbot (the Let's Encrypt client) on your server:**

`sudo apt update && sudo apt install certbot`

### **Obtain a Certificate**

Obtain your SSL certificate by running Certbot with the standalone plugin, which will temporarily start a web server on port 80 to perform the domain verification:

> Stop the Apache server if you are having issues executing this step

`sudo systemctl stop apache2`

`sudo certbot certonly --standalone -d yourdomain.com`

Replace yourdomain.com with your actual domain name. You'll need to ensure that port 80 on your server is open and that your DNS settings are correctly configured to point to your server's IP address.

### **Certificate Location**

The SSL certificate and private key will be stored in the following directory:

`/etc/letsencrypt/live/yourdomain.com/`

Here, you'll find fullchain.pem (the certificate plus the chain) and privkey.pem (the private key).

Copy these two files to the appropriate directory, so that the Pantos Service Node can access them:

```
# Don't forget to adjust your domain name

sudo cp /etc/letsencrypt/live/yourdomain.com/fullchain.pem /etc/pantos/service-node-fullchain.pem
sudo cp /etc/letsencrypt/live/yourdomain.com/privkey.pem /etc/pantos/service-node-privkey.pem
sudo chown pantos:pantos /etc/pantos/service-node-fullchain.pem
sudo chown pantos:pantos /etc/pantos/service-node-privkey.pem
sudo chmod 400 /etc/pantos/service-node-fullchain.pem
sudo chmod 400 /etc/pantos/service-node-privkey.pem
```

### Automating Certificate Renewal and Deployment

#### **Renewal Job**

Certbot will automatically set up a cron job or systemd timer to attempt to renew certificates that are near expiration. You can test the renewal process with:

`sudo certbot renew --dry-run`

#### **Post-Renewal Hook Script**

Create a script that will handle the deployment of the new certificate after renewal. Create a file with the following script:

`sudo nano /usr/local/bin/deploy_cert.sh`

#### **Insert the following code into deploy\_cert.sh:**

<pre><code><strong>DOMAIN="yourdomain.com"
</strong>PANTOS_CERT_PATH="/etc/pantos/service-node-fullchain.pem"
PANTOS_KEY_PATH="/etc/pantos/service-node-privkey.pem"

PANTOS_CERT_DIR="/etc/pantos"

# Stop the Pantos service before updating certificates
sudo systemctl stop pantos-service-node-server
sudo systemctl stop pantos-service-node-celery

# Copy the new cert and private key
cp "/etc/letsencrypt/live/$DOMAIN/fullchain.pem" "$PANTOS_CERT_PATH"
cp "/etc/letsencrypt/live/$DOMAIN/privkey.pem" "$PANTOS_KEY_PATH"

# Set permissions
sudo chown pantos:pantos /etc/pantos/service-node-fullchain.pem
sudo chown pantos:pantos /etc/pantos/service-node-privkey.pem
sudo chmod 400 /etc/pantos/service-node-fullchain.pem
sudo chmod 400 /etc/pantos/service-node-privkey.pem

# Start the Pantos service again
sudo systemctl start pantos-service-node-server
sudo systemctl start pantos-service-node-celery

</code></pre>

Replace yourdomain.com with your actual domain and adjust the paths if needed.

#### **Make the script executable:**

`sudo chmod +x /usr/local/bin/deploy_cert.sh`

#### **Certbot Hook Configuration**

Instruct Certbot to use this script after renewal by editing the renewal configuration file located at `/etc/letsencrypt/renewal/yourdomain.com.conf`.

#### **Add a post\_hook directive under the \[renewalparams] section:**

`[renewalparams] ... post_hook = /usr/local/bin/deploy_cert.sh`

Save and close the file. Certbot will now execute deploy\_cert.sh after each successful renewal.

## Step 3: Generating a Key with Geth for Ethereum-compatible Wallet

### Installing Geth

**Install Geth on your server:**

```
sudo apt-get install software-properties-common
sudo add-apt-repository -y ppa:ethereum/ethereum
sudo apt update
sudo apt install ethereum
```

### **Generate Ethereum Wallet**

Generate a new Ethereum account (this will create a new keypair):

`geth account new`

You will be prompted to create a passphrase. Keep it safe and remember it, as it is needed for the service node configuration.

### **Secure the Keystore File**

Locate the keystore file created by geth, which is typically located in the directory **\~/.ethereum/keystore.** Move this file to the location expected by the Pantos service node:

```
sudo mv ~/.ethereum/keystore/UTC--<timestamp>--<your-address> /etc/pantos/service-node.keystore
sudo chown pantos:pantos /etc/pantos/service-node.keystore
sudo chmod 400 /etc/pantos/service-node.keystore
```

Replace **timestamp** and **your-address** with the actual filename of your keystore file.

## Step 4: Configuring Service Node and Off-Chain Bids

Now that the SSL certificate and keystore are in place, it's time to configure your Service Node's parameters and bids for transactions. This involves mostly editing these configuration files: `/etc/pantos/service-node-config.env` and `/etc/pantos/service-node-bids.yml.`

We provide two ways to modify the app configuration, either through `service-node-config.env` or `service-node-config.yml`. We recommend using the `.env` file, as the `.yml` file is overwritten on every install.

Currently, you need to modify the `service-node-config.yml` only to set your domain:

```
url: www.yourdomain.com:8080 (remove: !ENV ${APP_URL})
```

While using the `.env` file you need to be aware that any fields containing certain special characters need to be wrapped around single quotes (e.g. `ETHEREUM_PRIVATE_KEY_PASSWORD='12$$#%R^'`).

### Adapt Service-Node-Config.env

You need to review and adapt the Service Node's configuration file appropriately before starting the Service Node instance:

`sudo nano /etc/pantos/service-node-config.env`



There are different ways to add your private key:

* Use Default location: `/etc/pantos/service-node.keystore`
* Define a custom location in the env file: `AVALANCHE_PRIVATE_KEY=/your/custompath/service-node.keystore`
* Add value directly in the env file: `AVALANCHE_PRIVATE_KEY='...'`

#### **In particular, make sure that:**

* All \<fill me> sections have been filled
* the PRIVATE\_KEY\_PASSWORD is the correct password for your keystore file
* the correct blockchains have been activated e.g `AVALANCHE_ACTIVE=true`

{% hint style="info" %}
All currently supported blockchains are active by default.
{% endhint %}

#### **Example configuration for the Avalanche testnet:**

```
##### Section: avalanche #####
# AVALANCHE_ACTIVE=
AVALANCHE_UNSTAKING_ADDRESS='<fill me>'
# AVALANCHE_PRIVATE_KEY=
AVALANCHE_PRIVATE_KEY_PASSWORD='<fill me>'
# AVALANCHE_PROVIDER=
# AVALANCHE_FALLBACK_PROVIDER=
# AVALANCHE_AVERAGE_BLOCK_TIME=
# AVALANCHE_PROVIDER_TIMEOUT=
# AVALANCHE_CHAIN_ID=
# AVALANCHE_HUB=
# AVALANCHE_FORWARDER=
# AVALANCHE_PAN_TOKEN=
# AVALANCHE_CONFIRMATIONS=
# AVALANCHE_MIN_ADAPTABLE_FEE_PER_GAS=
# AVALANCHE_MAX_TOTAL_FEE_PER_GAS=
# AVALANCHE_ADAPTABLE_FEE_INCREASE_FACTOR=
# AVALANCHE_BLOCKS_UNTIL_RESUBMISSION=
# AVALANCHE_STAKE=
```

### Adapt Pantos-Offchain-Bids.yaml

Each Service Node bid has to be added to the bids list in the configuration section of its source blockchain and contains:

* execution time in seconds
* fee for a Pantos transfer in Panini
* validity period in seconds

By default each blockchain route has two bids already configured, that you can adjust accordingly.

```
bnb_chain:
    ethereum:
      - execution_time: 400
        fee: 25000000000
        valid_period: 300
      - execution_time: 1000
        fee: 9500000000
        valid_period: 300
```

In this example, BNB Chain is the source, and Ethereum is the destination. This configuration activates the ability of your Service Node to handle transactions from BNB Chain to Ethereum.

#### **After the configuration has been adapted to your liking, start the Service Node instance with:**

```
sudo systemctl start pantos-service-node-server
sudo systemctl start pantos-service-node-celery
```

> **Remember:** You need at least 100.000 PAN and native coins for each blockchain that you want to serve!

Please reach out to the team if you need help getting the required amounts of PAN.

The log output of the Service Node is then available at `/var/log/pantos/service-node.log` for the web server and `/var/log/pantos/service-node-worker.log` for the worker process that asynchronously submits transfer requests to the blockchain networks.

If your Pantos Service Node setup is successful, you'll see confirmation in the log files indicating that the node is registered with the Pantos Hub. This means your node is now part of the Pantos network, ready to contribute to its operations.

For any issues during setup, please contact Pantos support for assistance. Thank you for contributing to the Pantos ecosystem!

## OPTIONAL Step 5: Custom Bid Plugins

### Introduction

Service Nodes include a mechanism for bid plugins, allowing you to define custom code to calculate fees for blockchain transfers. This step will guide you through the process of using and customizing these plugins.

### Default Bid Behavior

The service node comes with a default bid plugin that calculates fees based on a YAML configuration file.

**YAML Configuration File Location:** `/etc/pantos/offchain-bids.yaml`

This file contains predefined fees for various blockchain transfer pairs.

### Plugin Files Location

#### **Base Plugin:** Located at `/opt/pantos/service-node/virtual-environment/lib/python3.10/site-packages/pantos/servicenode/plugins/base.py`

This file has the abstract BidPlugin class.

#### **Bids Plugin:** Located at `/opt/pantos/service-node/virtual-environment/lib/python3.10/site-packages/pantos/servicenode/plugins/bids.py`

This file contains the default implementation that reads the YAML file.

### Understanding Bid Plugin Methods

#### **'get\_bids' Method:**

**Purpose:** This method is the heart of your bid plugin. It's where you define how your service node calculates the fees for transferring tokens between blockchains.

**How it Works:** The method needs to determine fees based on factors like market conditions, transaction complexity, and speed requirements. It returns two things: a list of Bid objects and a time interval in seconds. The Bid objects represent the fee details for each supported blockchain transfer. The time interval tells the service node how often to update these fees.

**Example:** If you want to adjust fees based on current token values or gas price fluctuations, you would code these rules in get\_bids.

#### **'accept\_bid' Method:**

**Purpose:** This method decides whether to accept or reject a transfer request based on the bid provided by the user.

**How it Works:** It examines the bid details submitted by a user wanting to make a transfer. You can write logic to check if the bid meets certain criteria, like minimum fee requirements or if the bid is valid considering current market prices.

**Example:** If there's a sudden spike in a token's value, and the bid no longer covers your operational costs, accept\_bid can reject the request.

### Customizing Your Bid Plugin

#### **Plan Your Strategy:**

Decide how you want your service node to calculate and accept fees. Consider factors like speed, market trends, and operational costs.

#### **Create Your Custom Plugin:**

* Go to the plugins directory.
* Create a Python file for your plugin.
* Inherit from BidPlugin: Extend the BidPlugin class in your custom file.
* Code your fee calculation and bid acceptance logic in these methods.

#### **Activate Your Plugin:**

* Update `/etc/pantos/service-node-config.yml` to point to your new plugin.
* Restart the service node.

{% hint style="info" %}
Every time you update your service node, you will need to redo this step.
{% endhint %}

Apply your changes by restarting the service node using the command:&#x20;

`sudo systemctl restart pantos-service-node-server`

`sudo systemctl restart pantos-service-node-celery`

#### **Verify Operation**

Check the logs to ensure your plugin is loaded and functioning as expected. Test with various scenarios to confirm the bid calculations are working correctly.

By following these detailed steps, even as a beginner, you can customize the bid plugin on your Pantos Service Node, tailoring it to your specific needs and market strategies.

## **Unregister your Node**

To unregister your Service Node from a specific blockchain, follow these updated steps:

1. **Edit Chains in the Config:**
   *   Open your service node's configuration file and adjust the settings for any chains you wish to unregister from:

       ```plaintext
       ETHEREUM_ACTIVE=true
       ETHEREUM_REGISTERED=false
       ```
2. **Restart Your Service Node:**
   *   After updating the configuration file, restart your service node to apply the changes:

       ```bash
       sudo systemctl start pantos-service-node-server
       sudo systemctl start pantos-service-node-celery
       ```
   * Once restarted, your service node will be unregistered, initiating the unbonding period.
3. **Unbonding Period:**
   * The unbonding period is a security measure lasting 7 days, during which the stake remains locked and cannot be used for any other purpose.
4.  **Withdrawal of Stake:**

    * After the unbonding period has passed, you can withdraw the stake by calling the `withdrawServiceNodeStake(address serviceNodeAddress)` function. This transaction can be initiated by either the service node address or a specified unstaking address found in your service node’s configuration (`unstaking_address`), which is ideal for operators who prefer a more secure setup, such as a hardware ledger.
    * For this step you can use for example the "[cast](https://book.getfoundry.sh/reference/cast/cast-send)" tool in Foundry or any other way to submit the transaction to the respective blockchains

    ```
    cast send --ledger <PantosHub address> "withdrawServiceNodeStake(address)" <service node address> --rpc-url <rpc url>
    ```


5. **Cancelling Unregistration:**
   *   If you decide to cancel the unregistration, reset the `ETHEREUM_REGISTERED` flag to true in the configuration and restart your service node:

       ```bash
       sudo systemctl restart pantos-service-node-server
       sudo systemctl restart pantos-service-node-celery
       ```
   * Doing so before withdrawing the stake will cancel the unregistration process, and the service node will resume its previous operational state.

