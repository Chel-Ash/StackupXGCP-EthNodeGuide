# StackupXGCP-EthNodeGuide

Hi, Welcome to this Guide Project. The Subject is to Run an Ethereum Validator Node Using Google Cloud Platform Services.

![stackup x gcp](https://cdn.hackernoon.com/images/4jLd9wAdOWQW3iTiKFVy3oWadmu1-taa3w47.jpeg)

I've created a Full Working Guide that walks you through the entire process involved from A - Z, which anyone can replicate to get a functioning node.

The Guide Entails the Following Pointers:
* Introduction to Blockchains (Ethereum)
* What Network Validators are
* Ethereum POS Upgrade and Implications for Validators
* Roles and Responsibilities  of Validators
* Important Info about Execution / Consensus Clients including the Tradeoffs
* Overview of GCP and Blockchain + Security Operational Services 
* Step-by-Step Process through Becoming a Validator on Ethereum ( Acquire Ether, Setup Node, Configuration, Maintenance etc )

In other words - This is a Guide Suitable for Complete Beginners to the Space of Ethereum, and Validators.

[VISIT MEDIUM GUIDE HERE](https://medium.com/@chel_koby/your-complete-guide-to-running-an-ethereum-validator-on-gcp-blockchain-node-in-2023-for-44e85e61f4fb)

NB: Having understanding of Basic Blockchain Concepts(Buying Tokens, Wallets, Networks etc) would help 


### Quick Start Setup n Commands
This Section contains the essential steps and configuration for a quick start if you can figure out the rest processes.

Using [Blockchain Node Engine (BNE)](https://console.cloud.google.com/blockchain-node-engine) Service in GCP Products, you are Spinning up a Node with Execution and Consensus Client Syncing up. All that's left after your Node Updates to the Network's State is to Connect your Validators - through provided RPC Endpoints & API. 

Think of this like a Plug-n-Play Option that gives you full control of Your Validators while ensuring 24/7 operation (while enabled)

1. Install Lighthouse
>`wget https://github.com/sigp/lighthouse/releases/download/v4.1.0/lighthouse-v4.1.0-x86_64-unknown-linux-gnu.tar.gz`

2. Import Validators Keys (after creating service acct n generating keys)
> `sudo lighthouse account validator import \  
 --network goerli \  
 --datadir /var/lib/lighthouse/validators \  
 --directory=$HOME/staking-deposit-cli/validator_keys \  
 --reuse-password`

3.  Create a validator.service file with Foll Values
  
> `[Unit]  
Description=Lighthouse Validator Client for Testnet Stackup X GCP  
Wants=network-online.target  
After=network-online.target  
Documentation=https://github.com/Chel-Ash/StackupXGCP-EthNodeGuide  `
  
> `[Service]  
Type=simple  
User=validator  
Group=validator  
Restart=on-failure  
RestartSec=3  
KillSignal=SIGINT  
TimeoutStopSec=900  
ExecStart=/usr/bin/sudo lighthouse vc \  
  --network goerli \  
  --beacon-nodes http://<BEACON NODE API ENDPOINT>?key=<API-KEY> \  
  --datadir /var/lib/lighthouse/validators \  
  --graffiti="Setup Eth Validator on GCP" \  
  --metrics \  
  --suggested-fee-recipient=<WITHDRAWAL ADDRESS EHER>`
  
>`[Install]  
WantedBy=multi-user.target`

4. Enable Auto-boot, Start, Check Logs of Your Validator

>sudo systemctl daemon-reload
sudo systemctl enable validator  
sudo systemctl start validator  
sudo systemctl status validator  
sudo journalctl -fu validator | ccze


## Thanks for Reading
<hr>

This is a Bounty Courtesy of & Sponsored by [Stackup](https://app.stackup.dev/) X GCP @ [Bounty Information](https://app.stackup.dev/bounty/running-an-ethereum-validator-node) 👏
