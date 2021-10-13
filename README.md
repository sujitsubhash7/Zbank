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

## Genesis Block Creation and Configuration

The genesis block will be created using puppeth, which is a tool buddled from the **Go Ethereum** bundle. This is the first step of the blockchain as the genesis block is the first block on which additional blocks can be added. 

cd to the **Blockchain-Tools** folder in the git bash terminal and type `.\puppeth`, which will show a prompt asking you to name the network. We named the network 'pups'. Follow the promts shown below and as shown in Figure 1. 
1) Name the network
2) Type 2 to pick the Configure new genesis option, then 1 to Create new genesis from scratch
3) Type 2 to choose the Clique (Proof of Authority) consensus algorithm
4) Select the number of seconds each block should take. You can hit enter to select the default period of 15 seconds.
5) Copy the addresses of node 1 and node 2 from the notepad and enter in sequence when prompted to enter the accounts that need to be sealed.
6) Copy the addresses of the nodes that need to be prefunded. As we are testing the transaction from node 1 to node 2, we will only prefund node 1. 
7) Select no for the next prompt to keep the genesis cleaner. 

![Genesis Block Creation Part1](/Screenshots/step1a.JPG)
Figure 1. Genesis Block Creation Part1

8) Specify your chain ID. You will need this later to connect the custom network on the MyCrypto App. After this step the genesis configuration is stored in your local home directory.
9) Next select the "Manage existing genesis" and  "Export genesis configurations" options in the prompts as shown in Figure 2. 

![Genesis Block Configuration](/Screenshots/step1b.JPG)
Figure 2. Genesis Block Configuration

10) This will fail to create two of the files, but you only need `networkname.json`. See Figure 3.

![Files Created](/Screenshots/step1b2.JPG)
Figure 3. pups.json file

## Node Initialization and Mining

1) Using geth, initialize each node with the new `networkname.json` as shown in Figure 4.
```
./geth --datadir node1 init networkname.json
./geth --datadir node2 init networkname.json
```
The nodes can now be used to begin mining blocks.

2) To beging mining on node 1 run the following command. See Figure 4 for reference.
```
./geth --datadir node1 --unlock "SEALER_ONE_ADDRESS" --mine --rpc --allow-insecure-unlock
```
3) Copy the enode generated into a nodepad as we will need this to mine node 2.

![Node Initialization](/Screenshots/step2.JPG)
Figure 4. Nodes Initialization and Node 1 Mining

4) Open a new terminal window and run the following command as shown in Figure 5. 
```
./geth --datadir node2 --unlock "SEALER_TWO_ADDRESS" --mine --port 30304 --bootnodes "enode://SEALER_ONE_ENODE_ADDRESS@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock
```
5) Be sure to check that you are entering the correct node addresses (without Ox) and use the enode copied from step 3.

![Node Initialization](/Screenshots/step3.JPG)
Figure 5. Node 2 Mining

## Test Transaction between the Nodes

