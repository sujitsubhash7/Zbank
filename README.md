# Clique (Proof of Authority) Blockchain Development
This document will detail the development and testing of a Proof of Authority (POA) bloackchain.

## Install the Required Dependencies

1) Install the **MyCrypto Desktop App** through the link [https://download.mycrypto.com/](https://download.mycrypto.com/) for your operating system and follow the installation wizard. We need MyCrypto to make the transactions. 

2) Install **Go Ethereum"**. Go Ethereum is one of the three original implementations of the Ethereum protocol and will be used to create our the blockchain. Use the link [https://geth.ethereum.org/downloads/](https://geth.ethereum.org/downloads/) and download the **Geth & Tools 1.9.7**. Extract the downloaded file to the location where we will be creating the blockchain and rename the folder as 'Blockchain-Tools'.

## Node Creation

Create accounts for two nodes for the network with a separate datadir for each using geth by typing the commands into the Git Bash terminal as shown below:
```
./geth --datadir node1 account new
./geth --datadir node2 account new
```
Be sure to copy the public of the key for both nodes onto a notepad as you will need these later.

This will create node1 and node2 folders inside the 'Blockchain-Tools' folder. 

## Genesis Block Creation 

The genesis block will be created using puppeth, which is a tool buddled from the **Go Ethereum** bundle. This is the first step of the blockchain as the genesis block is the first block on which additional blocks can be added. 

cd to the **Blockchain-Tools** folder in the git bash terminal and type `.\puppeth`
