# Blockchain Testnet

Setup a custom testnet blockchain and send a test transaction to another account<br>

Use of terminal is required in the inital step for coding, and then the application<br> 
MyCrypto will be used<br>

Setup two new accounts (nodes) with seperate account numbers (node3/node4).  Using the<br> 
geth tool create the two different accounts in seperate folder using commands datadir and <br> 
geth.  The code looks as follows:<br>

./geth --datadir node3 account new<br>
./geth --datadir node4 account new<br>

Once created keep note of the public account numbers and store for retrieval.<br>

Now setup genesis block using puppeth tool (an Ethereum private network manager):<br>

The new genesis is called zbank, configure the puppeth tool to create a new genesis<br>
proof of authority conensus engine.  Set the block creation time to 15 seconds and <br>
Find the public address created in the above and configure into the genesis block.<br>  
Do not prefund the account as we want to mine.  Set a netowrk ID and store seperately<br>
for later referral.  The genesis block has now been configured.  Now we need to export<br>
genesis configuration specs into json files.  After configuring and exporting the configuration<br>
should look as follows:<br>

![top_20_teams](https://github.com/dowdlea86/blockchain_testnet/blob/main/Screenshots/zbanknet_config.png)

We need to initialize the nodes, using geth run the following code:

./geth init zbanknet/zbanknet.json --datadir node3 
./geth init zbanknet/zbanknet.json --datadir node4 

At this point we have succesfully wrote the gensis state.  Now we can use the nodes to begin mining.<br>
Use the following code to start the process:<br>:

./geth --datadir node3 --unlock "public key" --mine --rpc --allow-insecure-unlock<br>

In the public key section use the key from node3 in the intial step.  After the process<br>
has started to copy the enode information in the code and save seperatley.  This is important<br>
in the next step in "enode":<br>  

/geth --datadir node4 --unlock "public key" --mine --port 3034 --bootnodes "enode" --allow-insecure-unlock<br>

The "public key" is from the intial step.  The key must be from the second node created, in this case, node4.<br>
At this point the nodes should be up and running.  Now we will use the application MyCrypto for testing:





