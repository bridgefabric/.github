BridgeFabric is a decentralized serverless platform.  

### General Introduction

BridgeFabric is a distributed serverless system based on web3. It aims to build an easy-to-use decentralized governance serverless system, making every piece of function code generates value. Developers will write applications as WebAssembly, and dapr hosts the running of WebAssembly applications. dapr nodes use libp2p to discover and communicate with each other, and each dapr node has a unique identity, a nodeid, and dapr nodes that want to join the system to host applications need to stack first. Which dapr nodes are allowed to participate in the system, and which WebAssembly applications these nodes can run are determined by the on-chain governance contract. Users can write or select the applications they need to use and only need to pay for each call they make. webAssembly binary applications will be stored on ipfs.

### Architecture

The core purpose of BridgeFabric is to provide a serverless system with decentralized governance to combine the on-chain and off-chain data computing. Users with available computing resources can run worker nodes to provide computing power. Other users can purchase the actor from the market or write their own applications and pay only when these applications are actually called on the worker node.

BridgeFabric is modular designed, and each module can be upgraded so that it can be easily replaced when better technologies and implementations become available.

![image-20221029145512918](https://image-1255620078.cos.ap-nanjing.myqcloud.com/image-20221029145512918.png)

#### Worker Node

Users run functional nodes to earn money from idle arithmetic. Function nodes interact via the libp2p protocol to automatically discover other function nodes. The function nodes can run user-specified actor wasm programs on demand, and the function nodes automatically discover the nodes that can run the actor through the actor hosting contract. actor hosting contracts support a variety of ways to define the function nodes on which the actor runs, the two most basic ones being the specified run node method and the smart match method.

BridgeFabric maintains stability and reputation values for each function node, so that users can choose a node to run based on various considerations. (Stability and reputation system is under development)

#### Actor Code

Actor code is in WebAssembly binary format and is stored in distributed storage system. We are currently supporting Filecoin and IPFS as actor code storage.

Each actor has a unique identifier by which the actor can be called. It is not necessary to care about which node  executes it at the time of invocation. Its unique identifier is related to the content, and the unique identifier changes whenever the content changes. Since it is stored on the blockchain, the content of the actor can not be changed. When a actor is called, it is called only by the unique identifier.

#### Manager Node

> In development, before the manager node is completed, the user needs to trust the worker node (such as managing these worker node in consortium by several partners trusted each other) or implement the resultant trusted verification by  user themself.

Manager nodes are BridgeFabric's chain nodes that maintain the chain state and run system management contracts: reputation system contracts, node stability system contracts, woker node execute result verification contracts, node auto selection contracts, market contracts, etc.

##### Woker node execute result verification

The manager node has built-in verification contract, which also verifies the program results of worker nodes executing actor to prevent malicious or abnormal behavior of worker nodes.

#### DAO

BridgeFabric's governance contract which is unpluggable. It is currently deployed on polygon. It defines the management logic about this system.

#### Call private logic

BridgeFabric supports invoking user-private actors. Some applications that do not want to be hosted on public BridgeFabric worker node or considering about performance reasons, users can register their own node and its corresponding actor in the management contract. This allows the system to support calling private actor hosting on the node and also running by the same user.

#### Market

##### Worker Node Market

The worker node market displays all the nodes available to users and their key information, such as price, reputation, stability, region, etc. 

##### Actor Market

Actor market is a place to show all public actors avaliable to users.

Users can select wasm actor binary uploaded by other developers from the wasm marketplace.

Developers can upload their wasm actor binary, a functional description of the actor, and provide the corresponding test code for proof of completeness.

Developers can set the fee of the actor code, either free, fixed, or as a percentage of the total cost of a single call. Users who choose to use this actor code will paid only when they are using this actor code.







