# High Performance Blockchain (HPB) Unity SDK

With the High Performance Blockchain Unity SDK you can interact with the High Performance Blockchain ( https://hpb.io ) using Unity.
You will also find a fully working example game (Wang Gang) that utilize the High Performance Blockchain for storing each user's personal high score, the global high score, and it also reward users HPB whenever they end up on the global high score list through its contract on the High Performance Blockchain.
There is a public node available at https://node.myhpbwallet.com that you can use to interact with the High Performance Blockchain, and this is the node used in all of the included examples.

## SDK
HPB Unity SDK is originally based on Nethereum, which has then been modified to support HPB to take advantage of the low transaction costs and the high Transactions Per Seconds supported due to the hardware module used by HPB nodes, and the SDK also supports using the True Random Number Generator available on HPB through the hardware module on all nodes.
The HPB Unity SDK supports the latest version of Unity.

### Documentation
The High Performance Blockchain Unity SDK is fully backwards compatible with Nethereum, and you can locate the documentation here: https://nethereum.readthedocs.io/en/latest/


## Wang Gang
Wang Gang is a simple Proof of Concept game originally based on the Flappy Bird game created by Unity, and is here to show an example of how to integrate Unity with High Performance Blockchain. Whenever a player hits the highscore list, the player is awarded 1 HPB through the smart contract.

### How to get Wang Gang running
Wang Gang is a WebGL Game where players use the HPB Chrome Extension ( https://github.com/hpb-project/HPB_Chrome_Ext ) for signing transactions with the High Performance Blockchain.
Wang Gang is preconfigured with an account address (and its private key), along with a pre-created contract address on the High Performance Blockchain.
To get a local version up and running simply do the following:
1. Make a WebGL build and call it WangGang
2. Copy the index.html into the WangGang directory, replacing the existing one.
3. Either upload the files onto a hosting service (such as Github pages), or start a local http server (for example using: python -m SimpleHTTPServer 8000     and then heading to http://localhost:8000)

If you want to create your own version, you need to deploy a new contract on the High Performance Blockchain (see section about playerscore.sol below) and make adjustments in ScoreContractService.cs and TopScoreService.cs
A working demo can be found at http://game.myhpbwallet.com . To play the game, ensure you are using Chrome and got HPB Chrome Extension installed.


### Wang Gang files
Here is a summary of the High Performance Blockchain related files within the Wang Gang demo.

#### BlockNumber
This simply retrieves the current block number on High Performance Blockchain and displays it in-game.

#### GameControl
This controls the score and death of the player. If the player dies with a higher score than he or she previously had, then SubmitTopScore is enabled and the game will attempt to submit the score to the High Performance Blockchain.

#### TopScoreService
This makes all the calls to the High Performance Blockchain when it comes to getting current global top scores, the player's top score, as well as submitting new top scores.

#### ScoreContractService
This controls the integration with the Contract on High Performance Blockchain. It has the ABI (Application Binary Interface) and both queries and sets data in the High Performance Blockchain contract.

#### playerscore.sol
This is a basic high score solidity contract which .
You can deploy this using http://remix.dev together with HPB Chrome Extension.
1. Download HPB Chrome Extension from https://github.com/hpb-project/HPB_Chrome_Ext , create an account and transfer some HPB to it.
2. Visit http://remix.dev
3. Press "Add local file..." at the top left corner on the Remix window and select playerscore.sol
4. Select compiler version 0.4.10+commit.f0d539ae
5. Go to the Run tab, hit Deploy
6. Approve the contract transaction in HPB Chrome Extension
7. Take note of the Contract address
8. Input it into the ScoreContractService.cs file

#### index.html
When exporting a WebGL Game from within Unity, it does not support HPB Chrome Extension by default. You must call HPB Chrome Extension, which means you need to modify the index.html. A modified index.html file can be found in the Data directory. If you change the name of the build you must also change the within the index.html file ("var gameInstance = UnityLoader.instantiate("gameContainer", "Build/WangGang.json", {onProgress: UnityProgress});")

#### link.xml
When compiling to WebGL or IOS, you need to ensure that dlls are not stripped when running IL2CPP, which is done by adding a link.xml file. You can find a working link.xml file in the Assets directory.



## Other examples (inside the Data directory)

### EtherTransfer
This sample demonstrates how to transfer HPB from one account to another.

### TokenDeployAndSend
This sample covers all the steps of smart contract integration using the HRC20 standard token. It creates a new token on the High Performance Blockchain, and then sends 1000 to the specified address.
