# Blockchain Testnet

Setup a custom testnet blockchain and send a test transaction to another account<br>

Use of terminal is required in the inital step for coding, and then the application<br> 
MyCrypto is required<br>

Setup two new accounts (nodes) with seperate account numbers (node3/node4).  Using the<br> 
geth tool create the two different accounts in a seperate folder(directory) using commands<br>
datadir and geth.  The code looks as follows:<br>

./geth --datadir node3 account new<br>
./geth --datadir node4 account new<br>

Once created keep note of the public account numbers and store for retrieval.<br>

Now setup genesis block using the puppeth tool (an Ethereum private network manager):<br>

The new genesis is called zbank, configure the puppeth tool to create a new genesis<br>
proof of authority conensus engine.  Set the block creation time to 15 seconds and <br>
find the public address created in the above and configure into the genesis block.<br>  
Do not prefund the account as we want to mine.  Set a netowrk ID and store seperately<br>
for later referral.  The genesis block has now been configured.  Now we need to export<br>
genesis configuration specs into json files.  After configuring and exporting the configuration<br>
should look as follows:<br>

![zbanknet_config](https://github.com/dowdlea86/blockchain_testnet/blob/main/Screenshots/zbanknet_config.png)

We need to initialize the nodes, using geth, run the following code:<br>

./geth init zbanknet/zbanknet.json --datadir node3<br> 
./geth init zbanknet/zbanknet.json --datadir node4<br> 

At this point we have succesfully wrote the gensis state.  Now we can use the nodes to begin mining.<br>
Use the following code to start the process:<br>

./geth --datadir node3 --unlock "public key" --mine --rpc --allow-insecure-unlock<br>

In the public key section use the key from node3 in the intial step.  The mine flag instructs the<br> 
node to mine RPC stands for remote procedure call. This allowes the nodes to speak to each other in<br> 
the network.  The flag insercure unlock allows the nodes over security measures. After the process<br>
has started to copy the enode information in the code and save seperatley.  This is important in<br> 
the next step in "enode":<br>  

/geth --datadir node4 --unlock "public key" --mine --port 3034 --bootnodes "enode" --allow-insecure-unlock<br>

The "public key" is from the intial step.  The key must be from the second node created, in this case, node4.<br>
We need to specify another port, node3 used 3033, so in this case we need another port, 3034.<br>
Copy in the enode in node3 creation by creating a flag bootnodes "enode", put the enode address in the quotation<br>
marks. At this point the nodes should be up and running.  Now we will use the application MyCrypto for testing:<br>

In the application, we need to change the network to add a custom node with the custom information we set<br>
in the genisis.  In the open fields use the following infomration:<br>

Node Name: zbanknet<br>
Network: Customer<br>
Network Name: zbanknet<br>
Currency: ETH<br>
Chain ID: 3000 (Created in one of the inital steps)<br>
URL: http://127.0.0.1:8545 (This is the default RPC port)<br>

After clicking save and use, we need to access our wallet by clicking on the Keystore File icon<br>
Select wallet file inside Node3 directiory and put password that was created in an initial step.<br>
We can now see the account balance and want to run a test transaction.  Put in the public <br>
address from node 4 created above and put in an amount to send between accounts.  After sending<br>
the transaction should go from Pending to Succesful and the TX should look as follows:<br>

![transaction](https://github.com/dowdlea86/blockchain_testnet/blob/main/Screenshots/transaction.png)



