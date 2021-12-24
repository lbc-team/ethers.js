-----

Documentation: [html](https://docs.ethers.io/)

-----

Example: ERC-20 Contract
========================

Deploying a Contract
--------------------

#### **new ***ethers* . **ContractFactory**( abi , bytecode , signer )

Create a new [ContractFactory](/v5/api/contract/contract-factory/) which can deploy a contract to the blockchain.


```javascript
const bytecode = "0x608060405234801561001057600080fd5b506040516103bc3803806103bc83398101604081905261002f9161007c565b60405181815233906000907fddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef9060200160405180910390a333600090815260208190526040902055610094565b60006020828403121561008d578081fd5b5051919050565b610319806100a36000396000f3fe608060405234801561001057600080fd5b506004361061004c5760003560e01c8063313ce5671461005157806370a082311461006557806395d89b411461009c578063a9059cbb146100c5575b600080fd5b604051601281526020015b60405180910390f35b61008e610073366004610201565b6001600160a01b031660009081526020819052604090205490565b60405190815260200161005c565b604080518082018252600781526626bcaa37b5b2b760c91b6020820152905161005c919061024b565b6100d86100d3366004610222565b6100e8565b604051901515815260200161005c565b3360009081526020819052604081205482111561014b5760405162461bcd60e51b815260206004820152601a60248201527f696e73756666696369656e7420746f6b656e2062616c616e6365000000000000604482015260640160405180910390fd5b336000908152602081905260408120805484929061016a9084906102b6565b90915550506001600160a01b0383166000908152602081905260408120805484929061019790849061029e565b90915550506040518281526001600160a01b0384169033907fddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef9060200160405180910390a350600192915050565b80356001600160a01b03811681146101fc57600080fd5b919050565b600060208284031215610212578081fd5b61021b826101e5565b9392505050565b60008060408385031215610234578081fd5b61023d836101e5565b946020939093013593505050565b6000602080835283518082850152825b818110156102775785810183015185820160400152820161025b565b818111156102885783604083870101525b50601f01601f1916929092016040019392505050565b600082198211156102b1576102b16102cd565b500190565b6000828210156102c8576102c86102cd565b500390565b634e487b7160e01b600052601160045260246000fdfea2646970667358221220d80384ce584e101c5b92e4ee9b7871262285070dbcd2d71f99601f0f4fcecd2364736f6c63430008040033";

// A Human-Readable ABI; we only need to specify relevant fragments,
// in the case of deployment this means the constructor
const abi = [
    "constructor(uint totalSupply)"
];

const factory = new ethers.ContractFactory(abi, bytecode, signer)

// Deploy, setting total supply to 100 tokens (assigned to the deployer)
const contract = await factory.deploy(parseUnits("100"));

// The contract is not currentl live on the network yet, however
// its address is ready for us
contract.address
// '0x0f33B7CaD42da6A85BF3D4bE9191a3Cc6BF27F4d'

// Wait until the contract has been deployed before interacting
// with it; returns the receipt for the deployemnt transaction
await contract.deployTransaction.wait();
// {
//   blockHash: '0xac72a683d46dc683fcd986b2e889fb05e9b52ccbdb26e97168cfa4a36c700432',
//   blockNumber: 155,
//   byzantium: true,
//   confirmations: 1,
//   contractAddress: '0x0f33B7CaD42da6A85BF3D4bE9191a3Cc6BF27F4d',
//   cumulativeGasUsed: { BigNumber: "250842" },
//   effectiveGasPrice: { BigNumber: "2500000008" },
//   events: [
//     {
//       address: '0x0f33B7CaD42da6A85BF3D4bE9191a3Cc6BF27F4d',
//       blockHash: '0xac72a683d46dc683fcd986b2e889fb05e9b52ccbdb26e97168cfa4a36c700432',
//       blockNumber: 155,
//       data: '0x0000000000000000000000000000000000000000000000056bc75e2d63100000',
//       getBlock: [Function],
//       getTransaction: [Function],
//       getTransactionReceipt: [Function],
//       logIndex: 0,
//       removeListener: [Function],
//       topics: [
//         '0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef',
//         '0x0000000000000000000000000000000000000000000000000000000000000000',
//         '0x0000000000000000000000002143af6436d9ff82b5327fc94066a522b9cfac20'
//       ],
//       transactionHash: '0xe398d009f6289cf3cbcbd44eafda048498335ec0d8a4a252552144b91c7c4b81',
//       transactionIndex: 0
//     }
//   ],
//   from: '0x2143AF6436D9Ff82b5327Fc94066a522b9CFac20',
//   gasUsed: { BigNumber: "250842" },
//   logs: [
//     {
//       address: '0x0f33B7CaD42da6A85BF3D4bE9191a3Cc6BF27F4d',
//       blockHash: '0xac72a683d46dc683fcd986b2e889fb05e9b52ccbdb26e97168cfa4a36c700432',
//       blockNumber: 155,
//       data: '0x0000000000000000000000000000000000000000000000056bc75e2d63100000',
//       logIndex: 0,
//       topics: [
//         '0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef',
//         '0x0000000000000000000000000000000000000000000000000000000000000000',
//         '0x0000000000000000000000002143af6436d9ff82b5327fc94066a522b9cfac20'
//       ],
//       transactionHash: '0xe398d009f6289cf3cbcbd44eafda048498335ec0d8a4a252552144b91c7c4b81',
//       transactionIndex: 0
//     }
//   ],
//   logsBloom: '0x00000000000000000000000000020000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000800000000000000008000000000000001000000000000000000000001000000000020000000000000000000800000000000000000000000010000000000000000000000000000000000000000000000000000000000000000000000000000000000000000400000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000000000',
//   status: 1,
//   to: null,
//   transactionHash: '0xe398d009f6289cf3cbcbd44eafda048498335ec0d8a4a252552144b91c7c4b81',
//   transactionIndex: 0,
//   type: 2
// }
```

Connecting to a Contract
------------------------

### ERC20Contract

#### **new ***ethers* . **Contract**( address , abi , providerOrSigner )

Creating a new instance of a Contract connects to an existing contract by specifying its *address* on the blockchain, its *abi* (used to populate the class' methods) a *providerOrSigner*.

If a [Provider](/v5/api/providers/provider/) is given, the contract has only read-only access, while a [Signer](/v5/api/signer/#Signer) offers access to state manipulating methods.


```javascript
// A Human-Readable ABI; for interacting with the contract, we
// must include any fragment we wish to use
const abi = [
    // Read-Only Functions
    "function balanceOf(address owner) view returns (uint256)",
    "function decimals() view returns (uint8)",
    "function symbol() view returns (string)",

    // Authenticated Functions
    "function transfer(address to, uint amount) returns (bool)",

    // Events
    "event Transfer(address indexed from, address indexed to, uint amount)"
];

// This can be an address or an ENS name
const address = "0x0f33B7CaD42da6A85BF3D4bE9191a3Cc6BF27F4d";

// Read-Only; By connecting to a Provider, allows:
// - Any constant function
// - Querying Filters
// - Populating Unsigned Transactions for non-constant methods
// - Estimating Gas for non-constant (as an anonymous sender)
// - Static Calling non-constant methods (as anonymous sender)
const erc20 = new ethers.Contract(address, abi, provider);

// Read-Write; By connecting to a Signer, allows:
// - Everything from Read-Only (except as Signer, not anonymous)
// - Sending transactions for non-constant functions
const erc20_rw = new ethers.Contract(address, abi, signer);
```

Properties
----------

#### *erc20* . **address** => *string< [Address](/v5/api/utils/address/#address) >*

This is the address (or ENS name) the contract was constructed with.


#### *erc20* . **resolvedAddress** => *string< [Address](/v5/api/utils/address/#address) >*

This is a promise that will resolve to the address the **Contract** object is attached to. If an [Address](/v5/api/utils/address/#address) was provided to the constructor, it will be equal to this; if an ENS name was provided, this will be the resolved address.


#### *erc20* . **deployTransaction** => *[TransactionResponse](/v5/api/providers/types/#providers-TransactionResponse)*

If the **Contract** object is the result of a ContractFactory deployment, this is the transaction which was used to deploy the contract.


#### *erc20* . **interface** => *[Interface](/v5/api/utils/abi/interface/)*

This is the ABI as an [Interface](/v5/api/utils/abi/interface/).


#### *erc20* . **provider** => *[Provider](/v5/api/providers/provider/)*

If a provider was provided to the constructor, this is that provider. If a signer was provided that had a [Provider](/v5/api/providers/provider/), this is that provider.


#### *erc20* . **signer** => *[Signer](/v5/api/signer/#Signer)*

If a signer was provided to the constructor, this is that signer.


Methods
-------

#### *erc20* . **attach**( addressOrName ) => *[Contract](/v5/api/contract/contract/)*

Returns a new instance of the **Contract** attached to a new address. This is useful if there are multiple similar or identical copies of a Contract on the network and you wish to interact with each of them.


#### *erc20* . **connect**( providerOrSigner ) => *[Contract](/v5/api/contract/contract/)*

Returns a new instance of the Contract, but connected to *providerOrSigner*.

By passing in a [Provider](/v5/api/providers/provider/), this will return a downgraded **Contract** which only has read-only access (i.e. constant calls).

By passing in a [Signer](/v5/api/signer/#Signer). this will return a **Contract** which will act on behalf of that signer.


#### *erc20* . **deployed**( ) => *Promise< Contract >*



#### *Contract* . **isIndexed**( value ) => *boolean*



Events
------

#### *erc20* . **queryFilter**( event [ , fromBlockOrBlockHash [ , toBlock ] ) => *Promise< Array< Event > >*

Return Events that match the *event*.


#### *erc20* . **listenerCount**( [ event ] ) => *number*

Return the number of listeners that are subscribed to *event*. If no event is provided, returns the total count of all events.


#### *erc20* . **listeners**( event ) => *Array< Listener >*

Return a list of listeners that are subscribed to *event*.


#### *erc20* . **off**( event , listener ) => *this*

Unsubscribe *listener* to *event*.


#### *erc20* . **on**( event , listener ) => *this*

Subscribe to *event* calling *listener* when the event occurs.


#### *erc20* . **once**( event , listener ) => *this*

Subscribe once to *event* calling *listener* when the event occurs.


#### *erc20* . **removeAllListeners**( [ event ] ) => *this*

Unsubscribe all listeners for *event*. If no event is provided, all events are unsubscribed.


Meta-Class Methods
------------------

#### *erc20* . **decimals**( [ overrides ] ) => *Promise< number >*

Returns the number of decimal places used by this ERC-20 token. This can be used with [parseUnits](/v5/api/utils/display-logic/#utils-parseUnits) when taking input from the user or [formatUnits](utils-formatunits] when displaying the token amounts in the UI.


```javascript
await erc20.decimals();
// 18
```

#### *erc20* . **balanceOf**( owner [ , overrides ] ) => *Promise< [BigNumber](/v5/api/utils/bignumber/) >*

Returns the balance of *owner* for this ERC-20 token.


```javascript
await erc20.balanceOf(signer.getAddress())
// { BigNumber: "100000000000000000000" }
```

#### *erc20* . **symbol**( [ overrides ] ) => *Promise< string >*

Returns the symbol of the token.


```javascript
await erc20.symbol();
// 'MyToken'
```

#### *erc20_rw* . **transfer**( target , amount [ , overrides ] ) => *Promise< [TransactionResponse](/v5/api/providers/types/#providers-TransactionResponse) >*

Transfers *amount* tokens to *target* from the current signer. The return value (a boolean) is inaccessible during a write operation using a transaction. Other techniques (such as events) are required if this value is required. On-chain contracts calling the `transfer` function have access to this result, which is why it is possible.


```javascript
// Before...
formatUnits(await erc20_rw.balanceOf(signer.getAddress()));
// '100.0'

// Transfer 1.23 tokens to the ENS name "ricmoo.eth"
tx = await erc20_rw.transfer("ricmoo.eth", parseUnits("1.23"));
// {
//   accessList: [],
//   chainId: 31337,
//   confirmations: 0,
//   data: '0xa9059cbb0000000000000000000000005555763613a12d8f3e73be831dff8598089d3dca0000000000000000000000000000000000000000000000001111d67bb1bb0000',
//   from: '0x2143AF6436D9Ff82b5327Fc94066a522b9CFac20',
//   gasLimit: { BigNumber: "51558" },
//   gasPrice: null,
//   hash: '0xe6a39827adf9c1a65fab139f30f68f85b398eab84971b7a838a56810ddcc75ff',
//   maxFeePerGas: { BigNumber: "2500000016" },
//   maxPriorityFeePerGas: { BigNumber: "2500000000" },
//   nonce: 2,
//   r: '0x1761da02d382a47c2287a60a3ca8fc9d4352522e1488df7b2b98b7e14a9642fa',
//   s: '0x39ebe02915f69ff3654a72f98481f9e4b08af6e69cc7e3d51486613c4d75fb8f',
//   to: '0x0f33B7CaD42da6A85BF3D4bE9191a3Cc6BF27F4d',
//   type: 2,
//   v: 0,
//   value: { BigNumber: "0" },
//   wait: [Function]
// }

// Wait for the transaction to be mined...
await tx.wait();
// {
//   blockHash: '0xe81a4efab651d041b0f76b26f9431dba64f98fc12155f49f959abd68fc9e60a1',
//   blockNumber: 156,
//   byzantium: true,
//   confirmations: 1,
//   contractAddress: null,
//   cumulativeGasUsed: { BigNumber: "51558" },
//   effectiveGasPrice: { BigNumber: "2500000008" },
//   events: [
//     {
//       address: '0x0f33B7CaD42da6A85BF3D4bE9191a3Cc6BF27F4d',
//       args: [
//         '0x2143AF6436D9Ff82b5327Fc94066a522b9CFac20',
//         '0x5555763613a12D8F3e73be831DFf8598089d3dCa',
//         { BigNumber: "1230000000000000000" },
//         amount: { BigNumber: "1230000000000000000" },
//         from: '0x2143AF6436D9Ff82b5327Fc94066a522b9CFac20',
//         to: '0x5555763613a12D8F3e73be831DFf8598089d3dCa'
//       ],
//       blockHash: '0xe81a4efab651d041b0f76b26f9431dba64f98fc12155f49f959abd68fc9e60a1',
//       blockNumber: 156,
//       data: '0x0000000000000000000000000000000000000000000000001111d67bb1bb0000',
//       decode: [Function],
//       event: 'Transfer',
//       eventSignature: 'Transfer(address,address,uint256)',
//       getBlock: [Function],
//       getTransaction: [Function],
//       getTransactionReceipt: [Function],
//       logIndex: 0,
//       removeListener: [Function],
//       topics: [
//         '0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef',
//         '0x0000000000000000000000002143af6436d9ff82b5327fc94066a522b9cfac20',
//         '0x0000000000000000000000005555763613a12d8f3e73be831dff8598089d3dca'
//       ],
//       transactionHash: '0xe6a39827adf9c1a65fab139f30f68f85b398eab84971b7a838a56810ddcc75ff',
//       transactionIndex: 0
//     }
//   ],
//   from: '0x2143AF6436D9Ff82b5327Fc94066a522b9CFac20',
//   gasUsed: { BigNumber: "51558" },
//   logs: [
//     {
//       address: '0x0f33B7CaD42da6A85BF3D4bE9191a3Cc6BF27F4d',
//       blockHash: '0xe81a4efab651d041b0f76b26f9431dba64f98fc12155f49f959abd68fc9e60a1',
//       blockNumber: 156,
//       data: '0x0000000000000000000000000000000000000000000000001111d67bb1bb0000',
//       logIndex: 0,
//       topics: [
//         '0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef',
//         '0x0000000000000000000000002143af6436d9ff82b5327fc94066a522b9cfac20',
//         '0x0000000000000000000000005555763613a12d8f3e73be831dff8598089d3dca'
//       ],
//       transactionHash: '0xe6a39827adf9c1a65fab139f30f68f85b398eab84971b7a838a56810ddcc75ff',
//       transactionIndex: 0
//     }
//   ],
//   logsBloom: '0x00000000000000000800000000020000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000800000000000000008000000000000001000000000000000000000001000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000000000000000000000000000000400000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000000000001000000000200000000000000000000000000000000000000',
//   status: 1,
//   to: '0x0f33B7CaD42da6A85BF3D4bE9191a3Cc6BF27F4d',
//   transactionHash: '0xe6a39827adf9c1a65fab139f30f68f85b398eab84971b7a838a56810ddcc75ff',
//   transactionIndex: 0,
//   type: 2
// }

// After!
formatUnits(await erc20_rw.balanceOf(signer.getAddress()));
// '98.77'

formatUnits(await erc20_rw.balanceOf("ricmoo.eth"));
// '1.23'
```

#### *erc20* . *callStatic* . **transfer**( target , amount [ , overrides ] ) => *Promise< boolean >*

Performs a dry-run of transferring *amount* tokens to *target* from the current signer, without actually signing or sending a transaction.

This can be used to preflight check that a transaction will be successful.


```javascript
// The signer has enough tokens to send, so true is returned
await erc20_rw.callStatic.transfer("ricmoo.eth", parseUnits("1.23"));
// true

// A random address does not have enough tokens to
// send, in which case the contract throws an error
erc20_random = erc20_rw.connect(randomWallet);
await erc20_random.callStatic.transfer("ricmoo.eth", parseUnits("1.23"));
// [Error: missing revert data in call exception] {
//   code: 'CALL_EXCEPTION',
//   data: '0x',
//   error: Error: processing response error (body="{\"jsonrpc\":\"2.0\",\"id\":71,\"error\":{\"code\":-32603,\"message\":\"Error: VM Exception while processing transaction: reverted with reason string 'insufficient token balance'\"}}", error={"code":-32603}, requestBody="{\"method\":\"eth_call\",\"params\":[{\"from\":\"0x840a9391fea66e1cc09608944dd42df7ac5530e9\",\"to\":\"0x0f33b7cad42da6a85bf3d4be9191a3cc6bf27f4d\",\"data\":\"0xa9059cbb0000000000000000000000005555763613a12d8f3e73be831dff8598089d3dca0000000000000000000000000000000000000000000000001111d67bb1bb0000\"},\"latest\"],\"id\":71,\"jsonrpc\":\"2.0\"}", requestMethod="POST", url="http://localhost:8545", code=SERVER_ERROR, version=web/5.5.1)
//       at Logger.makeError (/Users/xiaonahe/Desktop/ethers.js/packages/logger/lib/index.js:199:21)
//       at Logger.throwError (/Users/xiaonahe/Desktop/ethers.js/packages/logger/lib/index.js:208:20)
//       at /Users/xiaonahe/Desktop/ethers.js/packages/web/lib/index.js:301:32
//       at step (/Users/xiaonahe/Desktop/ethers.js/packages/web/lib/index.js:33:23)
//       at Object.next (/Users/xiaonahe/Desktop/ethers.js/packages/web/lib/index.js:14:53)
//       at fulfilled (/Users/xiaonahe/Desktop/ethers.js/packages/web/lib/index.js:5:58)
//       at processTicksAndRejections (internal/process/task_queues.js:97:5) {
//     body: `{"jsonrpc":"2.0","id":71,"error":{"code":-32603,"message":"Error: VM Exception while processing transaction: reverted with reason string 'insufficient token balance'"}}`,
//     code: 'SERVER_ERROR',
//     error: Error: Error: VM Exception while processing transaction: reverted with reason string 'insufficient token balance'
//         at getResult (/Users/xiaonahe/Desktop/ethers.js/packages/providers/lib/json-rpc-provider.js:142:21)
//         at processJsonFunc (/Users/xiaonahe/Desktop/ethers.js/packages/web/lib/index.js:344:22)
//         at /Users/xiaonahe/Desktop/ethers.js/packages/web/lib/index.js:276:46
//         at step (/Users/xiaonahe/Desktop/ethers.js/packages/web/lib/index.js:33:23)
//         at Object.next (/Users/xiaonahe/Desktop/ethers.js/packages/web/lib/index.js:14:53)
//         at fulfilled (/Users/xiaonahe/Desktop/ethers.js/packages/web/lib/index.js:5:58)
//         at processTicksAndRejections (internal/process/task_queues.js:97:5) {
//       code: -32603,
//       data: undefined
//     },
//     reason: 'processing response error',
//     requestBody: '{"method":"eth_call","params":[{"from":"0x840a9391fea66e1cc09608944dd42df7ac5530e9","to":"0x0f33b7cad42da6a85bf3d4be9191a3cc6bf27f4d","data":"0xa9059cbb0000000000000000000000005555763613a12d8f3e73be831dff8598089d3dca0000000000000000000000000000000000000000000000001111d67bb1bb0000"},"latest"],"id":71,"jsonrpc":"2.0"}',
//     requestMethod: 'POST',
//     url: 'http://localhost:8545'
//   },
//   reason: 'missing revert data in call exception'
// }
```

#### *erc20* . *estimateGas* . **transfer**( target , amount [ , overrides ] ) => *Promise< [BigNumber](/v5/api/utils/bignumber/) >*

Returns an estimate for how many units of gas would be required to transfer *amount* tokens to *target*.


```javascript
await erc20_rw.estimateGas.transfer("ricmoo.eth", parseUnits("1.23"));
// { BigNumber: "34458" }
```

#### *erc20* . *populateTransaction* . **transfer**( target , amount [ , overrides ] ) => *Promise< [UnsignedTx](/v5/api/utils/transactions/#UnsignedTransaction) >*

Returns an [UnsignedTransaction](/v5/api/utils/transactions/#UnsignedTransaction) which could be signed and submitted to the network to transaction *amount* tokens to *target*.


```javascript
await erc20_rw.populateTransaction.transfer("ricmoo.eth", parseUnits("1.23"));
// {
//   data: '0xa9059cbb0000000000000000000000005555763613a12d8f3e73be831dff8598089d3dca0000000000000000000000000000000000000000000000001111d67bb1bb0000',
//   from: '0x2143AF6436D9Ff82b5327Fc94066a522b9CFac20',
//   to: '0x0f33B7CaD42da6A85BF3D4bE9191a3Cc6BF27F4d'
// }
```

#### Note on Estimating and Static Calling

When you perform a static call, the current state is taken into account as best as Ethereum can determine. There are many cases where this can provide false positives and false negatives. The eventually consistent model of the blockchain also means there are certain consistency modes that cannot be known until an actual transaction is attempted.


Meta-Class Filters
------------------

#### *erc20* . *filters* . **Transfer**( [ fromAddress [ , toAddress ] ] ) => *Filter*

Returns a new Filter which can be used to [query](/v5/api/contract/example/#erc20-queryfilter) or to [subscribe/unsubscribe to events](/v5/api/contract/example/#erc20-events).

If *fromAddress* is null or not provided, then any from address matches. If *toAddress* is null or not provided, then any to address matches.


```javascript
filterFrom = erc20.filters.Transfer(signer.address);
// {
//   address: '0x0f33B7CaD42da6A85BF3D4bE9191a3Cc6BF27F4d',
//   topics: [
//     '0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef',
//     '0x0000000000000000000000002143af6436d9ff82b5327fc94066a522b9cfac20'
//   ]
// }

// Search for transfers *from* me in the last 10 blocks
logsFrom = await erc20.queryFilter(filterFrom, -10, "latest");
// [
//   {
//     address: '0x0f33B7CaD42da6A85BF3D4bE9191a3Cc6BF27F4d',
//     args: [
//       '0x2143AF6436D9Ff82b5327Fc94066a522b9CFac20',
//       '0x5555763613a12D8F3e73be831DFf8598089d3dCa',
//       { BigNumber: "1230000000000000000" },
//       amount: { BigNumber: "1230000000000000000" },
//       from: '0x2143AF6436D9Ff82b5327Fc94066a522b9CFac20',
//       to: '0x5555763613a12D8F3e73be831DFf8598089d3dCa'
//     ],
//     blockHash: '0xe81a4efab651d041b0f76b26f9431dba64f98fc12155f49f959abd68fc9e60a1',
//     blockNumber: 156,
//     data: '0x0000000000000000000000000000000000000000000000001111d67bb1bb0000',
//     decode: [Function],
//     event: 'Transfer',
//     eventSignature: 'Transfer(address,address,uint256)',
//     getBlock: [Function],
//     getTransaction: [Function],
//     getTransactionReceipt: [Function],
//     logIndex: 0,
//     removeListener: [Function],
//     removed: false,
//     topics: [
//       '0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef',
//       '0x0000000000000000000000002143af6436d9ff82b5327fc94066a522b9cfac20',
//       '0x0000000000000000000000005555763613a12d8f3e73be831dff8598089d3dca'
//     ],
//     transactionHash: '0xe6a39827adf9c1a65fab139f30f68f85b398eab84971b7a838a56810ddcc75ff',
//     transactionIndex: 0
//   }
// ]

// Note that the args providees the details of the event, each
// parameters is available positionally, and since our ABI
// included parameter names also by name
logsFrom[0].args
// [
//   '0x2143AF6436D9Ff82b5327Fc94066a522b9CFac20',
//   '0x5555763613a12D8F3e73be831DFf8598089d3dCa',
//   { BigNumber: "1230000000000000000" },
//   amount: { BigNumber: "1230000000000000000" },
//   from: '0x2143AF6436D9Ff82b5327Fc94066a522b9CFac20',
//   to: '0x5555763613a12D8F3e73be831DFf8598089d3dCa'
// ]
```

```javascript
filterTo = erc20.filters.Transfer(null, signer.address);
// {
//   address: '0x0f33B7CaD42da6A85BF3D4bE9191a3Cc6BF27F4d',
//   topics: [
//     '0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef',
//     null,
//     '0x0000000000000000000000002143af6436d9ff82b5327fc94066a522b9cfac20'
//   ]
// }

// Search for transfers *to* me in the last 10 blocks
// Note: the contract transferred totalSupply tokens to us
//       when it was deployed in its constructor
logsTo = await erc20.queryFilter(filterTo, -10, "latest");
// [
//   {
//     address: '0x0f33B7CaD42da6A85BF3D4bE9191a3Cc6BF27F4d',
//     args: [
//       '0x0000000000000000000000000000000000000000',
//       '0x2143AF6436D9Ff82b5327Fc94066a522b9CFac20',
//       { BigNumber: "100000000000000000000" },
//       amount: { BigNumber: "100000000000000000000" },
//       from: '0x0000000000000000000000000000000000000000',
//       to: '0x2143AF6436D9Ff82b5327Fc94066a522b9CFac20'
//     ],
//     blockHash: '0xac72a683d46dc683fcd986b2e889fb05e9b52ccbdb26e97168cfa4a36c700432',
//     blockNumber: 155,
//     data: '0x0000000000000000000000000000000000000000000000056bc75e2d63100000',
//     decode: [Function],
//     event: 'Transfer',
//     eventSignature: 'Transfer(address,address,uint256)',
//     getBlock: [Function],
//     getTransaction: [Function],
//     getTransactionReceipt: [Function],
//     logIndex: 0,
//     removeListener: [Function],
//     removed: false,
//     topics: [
//       '0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef',
//       '0x0000000000000000000000000000000000000000000000000000000000000000',
//       '0x0000000000000000000000002143af6436d9ff82b5327fc94066a522b9cfac20'
//     ],
//     transactionHash: '0xe398d009f6289cf3cbcbd44eafda048498335ec0d8a4a252552144b91c7c4b81',
//     transactionIndex: 0
//   }
// ]

// Note that the args providees the details of the event, each
// parameters is available positionally, and since our ABI
// included parameter names also by name
logsTo[0].args
// [
//   '0x0000000000000000000000000000000000000000',
//   '0x2143AF6436D9Ff82b5327Fc94066a522b9CFac20',
//   { BigNumber: "100000000000000000000" },
//   amount: { BigNumber: "100000000000000000000" },
//   from: '0x0000000000000000000000000000000000000000',
//   to: '0x2143AF6436D9Ff82b5327Fc94066a522b9CFac20'
// ]
```

```javascript
// Listen to incoming events from signer:
erc20.on(filterFrom, (from, to, amount, event) => {
  // The `from` will always be the signer address
});

// Listen to incoming events to signer:
erc20.on(filterTo, (from, to, amount, event) => {
  // The `to` will always be the signer address
});

// Listen to all Transfer events:
erc20.on("Transfer", (from, to, amount, event) => {
  // ...
});
```

