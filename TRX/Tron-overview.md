# Full Overview of TRON

## 1.1 Project repositories
### https://github.com/tronprotocol
- [Java-TRON](https://github.com/tronprotocol/java-tron) - main repository for TRON nodes
- [Documentation](https://github.com/tronprotocol/Documentation) - all documentation
- [TronDeployment](https://github.com/tronprotocol/TronDeployment) - deployment scripts and config files for java-tron

## 1.2 Block explorer
- https://tronscan.org - Created by [Rovak](https://github.com/Rovak)

## 1.3 TRON consensus algorithm
TRON adopts TPoS, an improved DPoS algorithm.

## 1.4 Block Producing Speed of TRON
The network currently produces 1 block per 3 seconds.

## 1.5 Transaction model
The adopted transaction model is the account model instead of the UTXO model. The smallest unit of TRX is sun, 1 TRX=1,000,000 sun. Currently, only one-to-one transaction services are available, meaning that one-to-many or many-to-one transactions are not supported.

## 1.6 Account model
One account has only one corresponding address, which is needed for transfers. The multi-signature mechanism is not yet implemented on the current version of network. There are three ways to create an account on the main blockchain.
```
a.  Create account with an existing account.
b.  Send TRX to a new address to create account.
c.  Send tokens to a new address to create account.
```

# 2. TRON’s network structure

## 2.1 Node types
There are three types of nodes on TRON’s network: Witnesses(Super Representatives), Full Nodes and Solidity Nodes. A witness is responsible for block production; a full node provides APIs, and broadcasts transactions and blocks; a solidity node synchronizes irrevocable blocks and provides inquiry APIs.

## 2.2 Mainnet and testnet

### Mainnet
- Block Explorer: https://tronscan.org
- Config: https://github.com/tronprotocol/TronDeployment/blob/master/main_net_config.conf

### Testnet
- Block Explorer: https://test.tronscan.org
- Config: https://github.com/tronprotocol/TronDeployment/blob/master/test_net_config.conf

# 3. Operation of node

## 3.1 Recommended hardware specifications
```
Minimum specifications for full node deployment
CPU：16-core
RAM：16G
Bandwidth：100M
DISK：10T
Recommended specifications for full node deployment
CPU：64-core or more 
RAM：64G or more 
Bandwidth：500M and more
DISK：20T or more

Minimum specifications for solidity node deployment
CPU：16-core
RAM：16G
Bandwidth：100M
DISK：10T
Recommended specifications for solidity node deployment
CPU：64-core or more
RAM：64G or more
Bandwidth：500M and more
DISK：20T or more

DISK capacity depends on the actual transaction volume after deployment, but it’s always better to leave some excess capacity.
```

## 3.2 Start the full node and solidity node
Please follow the guide here to configure and deploy both nodes: 
- https://github.com/tronprotocol/Documentation/blob/master/TRX/Solidity_and_Full_Node_Deployment_EN.md

We also provide a script to deploy fullnode and soliditynode:
- https://github.com/tronprotocol/TronDeployment/blob/master/README.md

# 4. TRON API
The TRON Nodes support both a gRPC Service and a HTTP Gateway

## 4.1 API Definition
Please see the protobuf protocol for the raw API.
- [Protobuf API](https://github.com/tronprotocol/protocol/blob/master/api/api.proto)
- [Protobuf Structures](https://github.com/tronprotocol/Documentation/blob/master/English_Documentation/TRON_Protocol/TRON_Protobuf_Protocol_document.md)

## 4.2 Explanation of APIs
### 4.2.1 gRPC interface
The Full Node and Solidity Nodes each run a gRPC service that you can connect to.

- [gRPC Tutorial](https://grpc.io/docs/)
- [gRPC API](https://github.com/tronprotocol/Documentation/blob/master/English_Documentation/TRON_Protocol/TRON_Wallet_RPC-API.md)

Please refer to the following two classes for a gRPC example in Java.
```
https://github.com/tronprotocol/wallet-cli/blob/master/src/main/java/org/tron/walletserver/WalletApi.java

https://github.com/tronprotocol/wallet-cli/blob/master/src/main/java/org/tron/walletserver/GrpcClient.java
```

### 4.2.2 HTTP Interface
The FullNode and SolidityNode both have an HTTP Service running on them. All parameters are encoded as `HEX` and returned as Hex or `base58check`. If you're trying to pass an address in, 
Having too many transactions will clog our network like Ethereum and may incur delays on transaction confirmation. To keep the network operating smoothly, TRON network grants every account a free pool of `Bandwidth points` for free transactions every 24 hours. To engage in transactions more frequently requires freezing TRX for additional bandwidth points, or paying the fee in TRX.

See also: https://github.com/tronprotocol/Documentation/blob/master/English_Documentation/TRON_Protocol/Mechanism_Introduction.md

## 5.1 Definition of Bandwidth Points
Transactions are transmitted and stored in the network in byte arrays. Bandwidth points consumed in a transaction equals the size of its byte array.
If the length of a byte array is 200 then the transaction consumes 200 

The amount of bandwidth points granted follows a formula:
```
Your Frozen TRX
---------------- * 54Gb of network bandwidth points available = Your available share of bandwidth points
Total Frozen TRX
```

## 5.3 Bandwidth points consumption rules
When there is available `Bandwidth points`, no TRX is charged. If a transaction fee is charged, it will be recorded in the fee field in the transaction results. If no transaction fee is charged, meaning that corresponding bandwidth points have been deducted, the fee field will read “0”. There will only be a service charge after a transaction has been written into the blockchain. For more information on the 
```

## 6.3 Java code demo
See: https://github.com/tronprotocol/wallet-cli/blob/master/src/main/java/org/tron/demo/ECKeyDemo.java



# 8. Calculation of transaction ID
Hash the Raw data of the transaction.
in java
```
Hash.sha256(transaction.getRawData().toByteArray())
```
in php  by William
```
try {
      
    } catch (Exception $e) 

## 10.2 Local construction
Based on your method of constructing a transaction you are required to populate all fields of a transaction to construct it locally. Please note that you will need to configure the details of reference block and expiration, so you will need to connect to the mainnet during transaction construction. We advise that you set the latest block on the full node as 
The Super Representatives(SR) take important roles to build k in sequence, and the top 127 SRs share 32 TRX proportional to the amount of votes they hold. This means that the top 27 SRs will be rewarded over 32 TRX per block.

All TRX holders 

See also: https://github.com/tronprotocol/Documentation/blob/master/English_Documentation/TRON_Blockchain_Explorer/Guide_to_voting_on_the_new_blockchain_explorer.md


# 14. Relevant files
See also: https://github.com/tronprotocol/Documentation#documentation-guide

