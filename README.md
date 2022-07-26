# EARC - CANONICAL CHAIN 
PRIVATE ETHREUM TEST NETWORK IN ETHEREUM BLOCKCHAIN
## DOCUMENTATION
Truffle and Ganache that can easily emulate Ethereum Node for Development Purposes. These fake Ethereum Node are an easy way to test application.They are just Emulators they provide the same interface as on Ethereum Node deployed in Public Ethereum Network, but Internally they work compeletly different.
  
**Step 1 :** Create the folder to host the database and accounts for our Private Node.
```
mkdir -p <name of the folder>/private
cd <name of the folder>/private
```
**Step 2 :** Before creating our Private Instance, Genesis Block must be Defined. Genesis Block is a block that will define the initial behaviou of our Blockchain Instance.

Creating a Genesis Block file from scartch acn be painful and reusing the exsisting one can be a problem if its version are older than the current installation of "GETH".To ensure that the Genesis Block file is compete with current versions of Geth. Create it using a tool called "PUPPETH".Puppeth is a Command line tool installed in parallel with Geth and provides features to Create and Monitor your own Ethereum Node.

Here we are using Puppeth to Create Genesis Block file.
```
sudo add-apt-repository -y ppa:ethereum/ethereum
```
```
sudo apt-get update
```
```
sudo apt-get install ethereum
```
```
Puppeth
```
In Puppeth we have to set the "Consensus Engine" that we want to use.A consensus Algorithm is a procedure through which all the peer of the Blockchain Network reach a common agreement about the Present State of the Distributed Ledger.So After the Process Genesis Block has been created but still it is in memory and it need to to be exported into a file.Now, we have our Genesis Block file, Let use it to initialize our Private Ethereum Node.

Private Node will be Created Using Geth-Command by using this Command we Will Initalize the node with the Genesis Block which is in the exported file.
```
geth --datadir . init <network Adminstrator name>.json
```
This above command creates 2 Directories, one for the "GETH CHAINDATA" and Another one is called "KEYSTORE".
Keystore will contain our Accounts of our Ethereum Node.
Now, we will create 3 Accounts that we will use during this setup
> Account 1 will receive Mining Rewards 

> Accounts 2 & 3 will act as a sender and receiver 

**Step 4 :** To create those Accounts we use GETH Commands and specify the path of our Private Node Data Directory.
```
geth --datadir . account new
```
**NOTE:** 
      Follow Step 3 and further more Create 2 Accounts.
      
Three Accounts are created and each account have their Unique Address and Private Keys of these Accounts are located under the Keystore folder.
```
geth --datadir . account list
```
**NOTE:**
      By default the first Account in Private Ethereum Node with the index 0 is the one will receive all the Mining Rewards.

Therefore we initialize Our Private Node and created 3 Accounts for it, but still the Node aren't Started.
Inorder to start the Private Ethereum Node and Mine the Blocks we have to create a Script that will require all the parameters to let us to Intreact with the Private Ethereum Node.

Use Atom to Create that Script Named <script name>.sh inside the Private Directory.
```
atom <script name>.sh
```
## Network Script.sh
```
geth --network id <id of the Ethereum Private Network> --mine --minethreads 2 --datadir "." --nodiscover --rpc --rpcport "8545" --port "30303" --rpccrosdomain --nat "any" --rpcapi eth,web3,personal,net --unlock 0 --password ./password.sec --ipcpath "<path to ipc file>"
```
	
**NOTE:**
	Create a password file accordingly
	
Then before running the file <script name>.sh we must turn it into the executable file and run.
```
chmod +x <script name>.sh
```
```
./<script name>.sh
```

So let Start the script, Now terminal shows the list of line says "GENERATING DAG PROGRESS" and in each line it have percentage element that shows the progress of the DAG GENERATION.
DAG (or) Directed Acyclic Graph is a Data Structure is needed by the Ethash Algorithm. DAG is Generated every 30,000 Blocks and Period of 30,000 blocks is called as an "EPOCH".


## ADDITIONAL CONTENT

To attach the Geth Console to the running Node, The below cmd will connect Private Node with the Geth Javascript Console.
```
geth attach
```
(or)
```
geth console
```
	
## GETH CONSOLE COMMAND LIST
1.To display the total no. of accounts in the Private Node with their Address.
```
eth.accounts 
``` 
2.To display the Address of Coinbase Account ( Account which receive Mining rewards ).
```
eth.coinbase
```
3.To display the Account balance of Coinbase Account.
``` 
eth.getBalance(eth.coinbase)
```
4.To display the Account balance of specific Account in our Private Node with their respective index no.
```
eth.getBalance(eth.accounts[<index of Account no.>])
```
5.To display the Account balance of Coinbase Account in terms of ETH.
```
web3.fromWei(eth.getBalance(eth.coinbase), "ether")
```
6.To display the Account balance of specific Account in our Private Node with their respective index no. in terms of ETH.
```
web3.fromWei(eth.getBalance(eth.accounts[<index of Account no.>]), "ether")
```
7.To stop Mining Process.
```
miner.stop()
```
8.To restart the Mining Process with no. of threads as its Parameter.
```
miner.start(<no. of threads>)
```
9.To get info of Chain Id.
```
net.version
```
10.To Initiate Transaction.
```
eth.sendTransaction({from:eth.coinbase,
		     to:eth.accounts[index no.],
		     value:web.toWei(<Transaction Amount>,"ether")})
```
------------------------------------------------------------------------------------------------------------
