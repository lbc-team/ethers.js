-----

Documentation: [html](https://docs.ethers.io/)

-----

Provider
========

#### Coming from Web3.js?

If you are coming from Web3.js, this is one of the biggest differences you will encounter using ethers.

The ethers library creates a strong division between the operation a **Provider** can perform and those of a [Signer](/v5/api/signer/#Signer), which Web3.js lumps together.

This separation of concerns and a stricted subset of Provider operations allows for a larger variety of backends, a more consistent API and ensures other libraries to operate without being able to rely on any underlying assumption.


Accounts Methods
----------------

#### *provider* . **getBalance**( address [ , blockTag = latest ] ) => *Promise< [BigNumber](/v5/api/utils/bignumber/) >*

Returns the balance of *address* as of the *blockTag* block height.


```javascript
await provider.getBalance("ricmoo.eth");
// { BigNumber: "15228086122772908421" }
```

#### *provider* . **getCode**( address [ , blockTag = latest ] ) => *Promise< string< [DataHexString](/v5/api/utils/bytes/#DataHexString) > >*

Returns the contract code of *address* as of the *blockTag* block height. If there is no contract currently deployed, the result is `0x`.


```javascript
await provider.getCode("registrar.firefly.eth");
// '0x606060405236156100885763ffffffff60e060020a60003504166369fe0e2d81146100fa578063704b6c021461010f57806379502c551461012d578063bed866f614610179578063c37067fa1461019e578063c66485b2146101ab578063d80528ae146101c9578063ddca3f43146101f7578063f2c298be14610219578063f3fef3a314610269575b6100f85b6000808052600760209081527f6d5257204ebe7d88fd91ae87941cb2dd9d8062b64ae5a2bd2d28ec40b9fbf6df80543490810190915560408051918252517fdb7750418f9fa390aaf85d881770065aa4adbe46343bcff4ae573754c829d9af929181900390910190a25b565b005b341561010257fe5b6100f860043561028a565b005b341561011757fe5b6100f8600160a060020a03600435166102ec565b005b341561013557fe5b61013d610558565b60408051600160a060020a0396871681526020810195909552928516848401526060840191909152909216608082015290519081900360a00190f35b341561018157fe5b61018c600435610580565b60408051918252519081900360200190f35b6100f8600435610595565b005b34156101b357fe5b6100f8600160a060020a03600435166105e6565b005b34156101d157fe5b6101d9610676565b60408051938452602084019290925282820152519081900360600190f35b34156101ff57fe5b61018c61068d565b60408051918252519081900360200190f35b6100f8600480803590602001908201803590602001908080601f0160208091040260200160405190810160405280939291908181526020018383808284375094965061069495505050505050565b005b341561027157fe5b6100f8600160a060020a0360043516602435610ab2565b005b60025433600160a060020a039081169116146102a65760006000fd5b600454604080519182526020820183905280517f854231545a00e13c316c82155f2b8610d638e9ff6ebc4930676f84a5af08a49a9281900390910190a160048190555b50565b60025433600160a060020a039081169116146103085760006000fd5b60025460408051600160a060020a039283168152918316602083015280517fbadc9a52979e89f78b7c58309537410c5e51d0f63a0a455efe8d61d2b474e6989281900390910190a16002805473ffffffffffffffffffffffffffffffffffffffff1916600160a060020a038381169190911790915560008054604080516020908101849052815160e060020a6302571be30281527f91d1777781884d03a6757a803996e38de2a42967fb37eeaca72729271025a9e26004820152915192909416936302571be39360248084019492938390030190829087803b15156103e957fe5b60325a03f115156103f657fe5b50505060405180519050600160a060020a0316631e83409a826000604051602001526040518263ffffffff1660e060020a0281526004018082600160a060020a0316600160a060020a03168152602001915050602060405180830381600087803b151561045f57fe5b60325a03f1151561046c57fe5b50506040805160008054600354602093840183905284517f0178b8bf00000000000000000000000000000000000000000000000000000000815260048101919091529351600160a060020a039091169450630178b8bf9360248082019493918390030190829087803b15156104dd57fe5b60325a03f115156104ea57fe5b505060408051805160035460025460e860020a62d5fa2b0284526004840191909152600160a060020a03908116602484015292519216925063d5fa2b0091604480830192600092919082900301818387803b151561054457fe5b60325a03f1151561055157fe5b5050505b50565b600054600354600254600454600154600160a060020a039485169492831692165b9091929394565b6000818152600760205260409020545b919050565b6000818152600760209081526040918290208054349081019091558251908152915183927fdb7750418f9fa390aaf85d881770065aa4adbe46343bcff4ae573754c829d9af92908290030190a25b50565b60025433600160a060020a039081169116146106025760006000fd5b60015460408051600160a060020a039283168152918316602083015280517f279875333405c968e401e3bc4e71d5f8e48728c90f4e8180ce28f74efb5669209281900390910190a16001805473ffffffffffffffffffffffffffffffffffffffff1916600160a060020a0383161790555b50565b600654600554600160a060020a033016315b909192565b6004545b90565b80516001820190600080808060048510806106af5750601485115b156106ba5760006000fd5b600093505b8484101561072a57855160ff16925060618310806106e05750607a8360ff16115b80156106fc575060308360ff1610806106fc575060398360ff16115b5b801561070d57508260ff16602d14155b156107185760006000fd5b6001909501945b6001909301926106bf565b60045434101561073a5760006000fd5b866040518082805190602001908083835b6020831061076a5780518252601f19909201916020918201910161074b565b51815160209384036101000a60001901801990921691161790526040805192909401829003822060035483528282018190528451928390038501832060008054948401819052865160e060020a6302571be3028152600481018390529651929a509098509650600160a060020a0390921694506302571be393602480820194509192919082900301818787803b15156107ff57fe5b60325a03f1151561080c57fe5b505060405151600160a060020a031691909114905061082b5760006000fd5b60008054600354604080517f06ab5923000000000000000000000000000000000000000000000000000000008152600481019290925260248201869052600160a060020a03308116604484015290519216926306ab59239260648084019382900301818387803b151561089a57fe5b60325a03f115156108a757fe5b505060008054600154604080517f1896f70a00000000000000000000000000000000000000000000000000000000815260048101879052600160a060020a0392831660248201529051919092169350631896f70a9260448084019391929182900301818387803b151561091657fe5b60325a03f1151561092357fe5b50506001546040805160e860020a62d5fa2b02815260048101859052600160a060020a033381166024830152915191909216925063d5fa2b009160448082019260009290919082900301818387803b151561097a57fe5b60325a03f1151561098757fe5b505060008054604080517f5b0fc9c300000000000000000000000000000000000000000000000000000000815260048101869052600160a060020a0333811660248301529151919092169350635b0fc9c39260448084019391929182900301818387803b15156109f357fe5b60325a03f11515610a0057fe5b505060058054349081019091556006805460010190556000838152600760209081526040918290208054840190558151600160a060020a03331681529081019290925280518493507f179ef3319e6587f6efd3157b34c8b357141528074bcb03f9903589876168fa149281900390910190a260408051348152905182917fdb7750418f9fa390aaf85d881770065aa4adbe46343bcff4ae573754c829d9af919081900360200190a25b50505050505050565b60025433600160a060020a03908116911614610ace5760006000fd5b604051600160a060020a0383169082156108fc029083906000818181858888f193505050501515610aff5760006000fd5b60408051600160a060020a03841681526020810183905281517fac375770417e1cb46c89436efcf586a74d0298fee9838f66a38d40c65959ffda929181900390910190a15b50505600a165627a7a723058205c3628c01dc80233f51979d91a76cec2a25d84e86c9838d34672734ca2232b640029'
```

#### *provider* . **getStorageAt**( addr , pos [ , blockTag = latest ] ) => *Promise< string< [DataHexString](/v5/api/utils/bytes/#DataHexString) > >*

Returns the `Bytes32` value of the position *pos* at address *addr*, as of the *blockTag*.


```javascript
await provider.getStorageAt("registrar.firefly.eth", 0)
// '0x000000000000000000000000314159265dd8dbb310642f98f50c066173c1259b'
```

#### *provider* . **getTransactionCount**( address [ , blockTag = latest ] ) => *Promise< number >*

Returns the number of transactions *address* has ever **sent**, as of *blockTag*. This value is required to be the nonce for the next transaction from *address* sent to the network.


```javascript
await provider.getTransactionCount("ricmoo.eth");
// 27
```

Blocks Methods
--------------

#### *provider* . **getBlock**( block ) => *Promise< [Block](/v5/api/providers/types/#providers-Block) >*

Get the *block* from the network, where the `result.transactions` is a list of transaction hashes.


```javascript
await provider.getBlock(100004)
// {
//   _difficulty: { BigNumber: "3849295379889" },
//   difficulty: 3849295379889,
//   extraData: '0x476574682f76312e302e312d39383130306634372f6c696e75782f676f312e34',
//   gasLimit: { BigNumber: "3141592" },
//   gasUsed: { BigNumber: "21000" },
//   hash: '0xf93283571ae16dcecbe1816adc126954a739350cd1523a1559eabeae155fbb63',
//   miner: '0x909755D480A27911cB7EeeB5edB918fae50883c0',
//   nonce: '0x1a455280001cc3f8',
//   number: 100004,
//   parentHash: '0x73d88d376f6b4d232d70dc950d9515fad3b5aa241937e362fdbfd74d1c901781',
//   timestamp: 1439799168,
//   transactions: [
//     '0x6f12399cc2cb42bed5b267899b08a847552e8c42a64f5eb128c1bcbd1974fb0c'
//   ]
// }
```

#### *provider* . **getBlockWithTransactions**( block ) => *Promise< [BlockWithTransactions](/v5/api/providers/types/#providers-BlockWithTransactions) >*

Get the *block* from the network, where the `result.transactions` is an Array of [TransactionResponse](/v5/api/providers/types/#providers-TransactionResponse) objects.


```javascript
await provider.getBlockWithTransactions(100004)
// {
//   _difficulty: { BigNumber: "3849295379889" },
//   difficulty: 3849295379889,
//   extraData: '0x476574682f76312e302e312d39383130306634372f6c696e75782f676f312e34',
//   gasLimit: { BigNumber: "3141592" },
//   gasUsed: { BigNumber: "21000" },
//   hash: '0xf93283571ae16dcecbe1816adc126954a739350cd1523a1559eabeae155fbb63',
//   miner: '0x909755D480A27911cB7EeeB5edB918fae50883c0',
//   nonce: '0x1a455280001cc3f8',
//   number: 100004,
//   parentHash: '0x73d88d376f6b4d232d70dc950d9515fad3b5aa241937e362fdbfd74d1c901781',
//   timestamp: 1439799168,
//   transactions: [
//     {
//       accessList: null,
//       blockHash: '0xf93283571ae16dcecbe1816adc126954a739350cd1523a1559eabeae155fbb63',
//       blockNumber: 100004,
//       chainId: 0,
//       confirmations: 13766987,
//       creates: null,
//       data: '0x',
//       from: '0xcf00A85f3826941e7A25BFcF9Aac575d40410852',
//       gasLimit: { BigNumber: "90000" },
//       gasPrice: { BigNumber: "54588778004" },
//       hash: '0x6f12399cc2cb42bed5b267899b08a847552e8c42a64f5eb128c1bcbd1974fb0c',
//       nonce: 25,
//       r: '0xb23adc880d3735e4389698dddc953fb02f1fa9b57e84d3510a2a4b3597ac2486',
//       s: '0x4e856f95c4e2828933246fb4765a5bfd2ca5959840643bef0e80b4e3a243d064',
//       to: '0xD9666150A9dA92d9108198a4072970805a8B3428',
//       transactionIndex: 0,
//       type: 0,
//       v: 27,
//       value: { BigNumber: "5000000000000000000" },
//       wait: [Function]
//     }
//   ]
// }
```

Ethereum Naming Service (ENS) Methods
-------------------------------------

#### *provider* . **getResolver**( name ) => *Promise< [EnsResolver](/v5/api/providers/provider/#EnsResolver) >*

Returns an EnsResolver instance which can be used to further inquire about specific entries for an ENS name.


```javascript
// See below (Resolver) for examples of using this object
const resolver = await provider.getResolver("ricmoo.eth");
```

#### *provider* . **lookupAddress**( address ) => *Promise< string >*

Performs a reverse lookup of the *address* in ENS using the *Reverse Registrar*. If the name does not exist, or the forward lookup does not match, `null` is returned.

An ENS name requries additional configuration to setup a reverse record, they are not automatically set up.


```javascript
await provider.lookupAddress("0x5555763613a12D8F3e73be831DFf8598089d3dCa");
// 'ricmoo.eth'
```

#### *provider* . **resolveName**( name ) => *Promise< string< [Address](/v5/api/utils/address/#address) > >*

Looks up the address of *name*. If the name is not owned, or does not have a *Resolver* configured, or the *Resolver* does not have an address configured, `null` is returned.


```javascript
await provider.resolveName("ricmoo.eth");
// '0x5555763613a12D8F3e73be831DFf8598089d3dCa'
```

EnsResolver
-----------

#### *resolver* . **name** => *string*

The name of this resolver.


#### *resolver* . **address** => *string< [Address](/v5/api/utils/address/#address) >*

The address of the Resolver.


#### *resolver* . **getAddress**( [ cointType = 60 ] ) => *Promise< string >*

Returns a Promise which resolves to the [EIP-2304](https://eips.ethereum.org/EIPS/eip-2304) multicoin address stored for the *coinType*. By default an Ethereum [Address](/v5/api/utils/address/#address) (`coinType = 60`) will be returned.


```javascript
// By default, looks up the Ethereum address
// (this will match provider.resolveName)
await resolver.getAddress();
// '0x5555763613a12D8F3e73be831DFf8598089d3dCa'

// Specify the coinType for other coin addresses (0 = Bitcoin)
await resolver.getAddress(0);
// '1RicMooMWxqKczuRCa5D2dnJaUEn9ZJyn'
```

#### *resolver* . **getContentHash**( ) => *Promise< string >*

Returns a Promise which resolves to any stored [EIP-1577](https://eips.ethereum.org/EIPS/eip-1577) content hash.


```javascript
await resolver.getContentHash();
// 'ipfs://QmdTPkMMBWQvL8t7yXogo7jq5pAcWg8J7RkLrDsWZHT82y'
```

#### *resolver* . **getText**( key ) => *Promise< string >*

Returns a Promise which resolves to any stored [EIP-634](https://eips.ethereum.org/EIPS/eip-634) text entry for *key*.


```javascript
await resolver.getText("email");
// 'me@ricmoo.com'

await resolver.getText("url");
// 'https://www.ricmoo.com/'

await resolver.getText("com.twitter");
// '@ricmoo'
```

Logs Methods
------------

#### *provider* . **getLogs**( filter ) => *Promise< Array< [Log](/v5/api/providers/types/#providers-Log) > >*

Returns the Array of [Log](/v5/api/providers/types/#providers-Log) matching the *filter*.

Keep in mind that many backends will discard old events, and that requests which are too broad may get dropped as they require too many resources to execute the query.


Network Status Methods
----------------------

#### *provider* . **getNetwork**( ) => *Promise< [Network](/v5/api/providers/types/#providers-Network) >*

Returns the [Network](/v5/api/providers/types/#providers-Network) this Provider is connected to.


```javascript
await provider.getNetwork()
// {
//   chainId: 1,
//   ensAddress: '0x00000000000C2E074eC69A0dFb2997BA6C7d2e1e',
//   name: 'homestead'
// }
```

#### *provider* . **getBlockNumber**( ) => *Promise< number >*

Returns the block number (or height) of the most recently mined block.


```javascript
await provider.getBlockNumber()
// 13866990
```

#### *provider* . **getGasPrice**( ) => *Promise< [BigNumber](/v5/api/utils/bignumber/) >*

Returns a *best guess* of the [Gas Price](/v5/concepts/gas/#gas-price) to use in a transaction.


```javascript
// The gas price (in wei)...
gasPrice = await provider.getGasPrice()
// { BigNumber: "62279088998" }

// ...often this gas price is easier to understand or
// display to the user in gwei
utils.formatUnits(gasPrice, "gwei")
// '62.279088998'
```

#### *provider* . **getFeeData**( ) => *Promise< [FeeData](/v5/api/providers/types/#providers-FeeData) >*

Returns the current recommended [FeeData](/v5/api/providers/types/#providers-FeeData) to use in a transaction.

For an EIP-1559 transaction, the `maxFeePerGas` and `maxPriorityFeePerGas` should be used.

For legacy transactions and networks which do not support EIP-1559, the `gasPrice` should be used.


```javascript
// The gas price (in wei)...
feeData = await provider.getFeeData()
// {
//   gasPrice: { BigNumber: "62279088998" },
//   maxFeePerGas: { BigNumber: "125058177996" },
//   maxPriorityFeePerGas: { BigNumber: "2500000000" }
// }

// ...often these values are easier to understand or
// display to the user in gwei
utils.formatUnits(feeData.maxFeePerGas, "gwei")
// '125.058177996'
```

#### *provider* . **ready** => *Promise< [Network](/v5/api/providers/types/#providers-Network) >*

Returns a Promise which will stall until the network has heen established, ignoring errors due to the target node not being active yet.

This can be used for testing or attaching scripts to wait until the node is up and running smoothly.


Transactions Methods
--------------------

#### *provider* . **call**( transaction [ , blockTag = latest ] ) => *Promise< string< [DataHexString](/v5/api/utils/bytes/#DataHexString) > >*

Returns the result of executing the *transaction*, using *call*. A call does not require any ether, but cannot change any state. This is useful for calling getters on Contracts.


```javascript
await provider.call({
  // ENS public resovler address
  to: "0x4976fb03C32e5B8cfe2b6cCB31c09Ba78EBaBa41",

  // `function addr(namehash("ricmoo.eth")) view returns (address)`
  data: "0x3b3b57debf074faa138b72c65adbdcfb329847e4f2c04bde7f7dd7fcad5a52d2f395a558"
});
// '0x0000000000000000000000005555763613a12d8f3e73be831dff8598089d3dca'
```

#### *provider* . **estimateGas**( transaction ) => *Promise< [BigNumber](/v5/api/utils/bignumber/) >*

Returns an estimate of the amount of gas that would be required to submit *transaction* to the network.

An estimate may not be accurate since there could be another transaction on the network that was not accounted for, but after being mined affected relevant state.


```javascript
await provider.estimateGas({
  // Wrapped ETH address
  to: "0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2",

  // `function deposit() payable`
  data: "0xd0e30db0",

  // 1 ether
  value: parseEther("1.0")
});
// { BigNumber: "27938" }
```

#### *provider* . **getTransaction**( hash ) => *Promise< [TransactionResponse](/v5/api/providers/types/#providers-TransactionResponse) >*

Returns the transaction with *hash* or null if the transaction is unknown.

If a transaction has not been mined, this method will search the transaction pool. Various backends may have more restrictive transaction pool access (e.g. if the gas price is too low or the transaction was only recently sent and not yet indexed) in which case this method may also return null.


```javascript
await provider.getTransaction("0x5b73e239c55d790e3c9c3bbb84092652db01bb8dbf49ccc9e4a318470419d9a0");
// {
//   accessList: null,
//   blockHash: '0x8a179bc6cb299f936c4fd614995e62d597ec6108b579c23034fb220967ceaa94',
//   blockNumber: 12598244,
//   chainId: 1,
//   confirmations: 1268747,
//   creates: '0x733aF852514e910E2f8af40d61E00530377889E9',
//   data: '0x608060405234801561001057600080fd5b5060405161062438038061062483398101604081905261002f916100cd565b60405163c47f002760e01b815260206004820152600d60248201526c0daead8e8d2c6c2d8d85ccae8d609b1b60448201526001600160a01b0382169063c47f002790606401602060405180830381600087803b15801561008e57600080fd5b505af11580156100a2573d6000803e3d6000fd5b505050506040513d601f19601f820116820180604052508101906100c691906100fb565b5050610113565b6000602082840312156100de578081fd5b81516001600160a01b03811681146100f4578182fd5b9392505050565b60006020828403121561010c578081fd5b5051919050565b610502806101226000396000f3fe608060405234801561001057600080fd5b506004361061002b5760003560e01c80634c0770b914610030575b600080fd5b61004361003e366004610309565b61005b565b60405161005293929190610389565b60405180910390f35b600060608085841461006c57600080fd5b8567ffffffffffffffff81111561009357634e487b7160e01b600052604160045260246000fd5b6040519080825280602002602001820160405280156100bc578160200160208202803683370190505b5091508567ffffffffffffffff8111156100e657634e487b7160e01b600052604160045260246000fd5b60405190808252806020026020018201604052801561011957816020015b60608152602001906001900390816101045790505b50905060005b86811015610235576101cd8a8a8a8a8581811061014c57634e487b7160e01b600052603260045260246000fd5b905060200201602081019061016191906102db565b89898681811061018157634e487b7160e01b600052603260045260246000fd5b90506020028101906101939190610460565b8080601f01602080910402602001604051908101604052809392919081815260200183838082843760009201919091525061024592505050565b8483815181106101ed57634e487b7160e01b600052603260045260246000fd5b6020026020010184848151811061021457634e487b7160e01b600052603260045260246000fd5b6020908102919091010191909152528061022d816104a5565b91505061011f565b5043925096509650969350505050565b6000606060405190506000815260208101604052600080845160208601878afa9150843d101561028857603f3d01601f191681016040523d81523d6000602083013e5b94509492505050565b60008083601f8401126102a2578182fd5b50813567ffffffffffffffff8111156102b9578182fd5b6020830191508360208260051b85010111156102d457600080fd5b9250929050565b6000602082840312156102ec578081fd5b81356001600160a01b0381168114610302578182fd5b9392505050565b60008060008060008060808789031215610321578182fd5b8635955060208701359450604087013567ffffffffffffffff80821115610346578384fd5b6103528a838b01610291565b9096509450606089013591508082111561036a578384fd5b5061037789828a01610291565b979a9699509497509295939492505050565b60006060820185835260206060818501528186518084526080860191508288019350845b818110156103c9578451835293830193918301916001016103ad565b5050848103604086015285518082528282019350600581901b82018301838801865b8381101561045057601f1980868503018852825180518086528a5b81811015610421578281018a01518782018b01528901610406565b81811115610431578b8a83890101525b5098880198601f019091169390930186019250908501906001016103eb565b50909a9950505050505050505050565b6000808335601e19843603018112610476578283fd5b83018035915067ffffffffffffffff821115610490578283fd5b6020019150368190038213156102d457600080fd5b60006000198214156104c557634e487b7160e01b81526011600452602481fd5b506001019056fea264697066735822122083b5dc25b3c9256aa4244eddaf9e4b5fccd09a45ec4e0174f2c900de7144602d64736f6c63430008040033000000000000000000000000084b1c3c81545d370f3634392de611caabff8148',
//   from: '0x8ba1f109551bD432803012645Ac136ddd64DBA72',
//   gasLimit: { BigNumber: "443560" },
//   gasPrice: { BigNumber: "10100000000" },
//   hash: '0x5b73e239c55d790e3c9c3bbb84092652db01bb8dbf49ccc9e4a318470419d9a0',
//   nonce: 745,
//   r: '0xaf2b969de6dfb234fb8843f47a029636abb1ef52f26bb8bb615bbabcf23808e9',
//   s: '0x3dd61cd8df015e0af5689a249dd3224ee71f2b04917b7b4c14f7e68bb3a4ec17',
//   to: null,
//   transactionIndex: 315,
//   type: 0,
//   v: 38,
//   value: { BigNumber: "0" },
//   wait: [Function]
// }
```

#### *provider* . **getTransactionReceipt**( hash ) => *Promise< [TransactionReceipt](/v5/api/providers/types/#providers-TransactionReceipt) >*

Returns the transaction receipt for *hash* or null if the transaction has not been mined.

To stall until the transaction has been mined, consider the `waitForTransaction` method below.


```javascript
await provider.getTransactionReceipt("0x5b73e239c55d790e3c9c3bbb84092652db01bb8dbf49ccc9e4a318470419d9a0");
// {
//   blockHash: '0x8a179bc6cb299f936c4fd614995e62d597ec6108b579c23034fb220967ceaa94',
//   blockNumber: 12598244,
//   byzantium: true,
//   confirmations: 1268747,
//   contractAddress: '0x733aF852514e910E2f8af40d61E00530377889E9',
//   cumulativeGasUsed: { BigNumber: "12102324" },
//   effectiveGasPrice: { BigNumber: "10100000000" },
//   from: '0x8ba1f109551bD432803012645Ac136ddd64DBA72',
//   gasUsed: { BigNumber: "443560" },
//   logs: [
//     {
//       address: '0x00000000000C2E074eC69A0dFb2997BA6C7d2e1e',
//       blockHash: '0x8a179bc6cb299f936c4fd614995e62d597ec6108b579c23034fb220967ceaa94',
//       blockNumber: 12598244,
//       data: '0x000000000000000000000000084b1c3c81545d370f3634392de611caabff8148',
//       logIndex: 160,
//       topics: [
//         '0xce0457fe73731f824cc272376169235128c118b49d344817417c6d108d155e82',
//         '0x91d1777781884d03a6757a803996e38de2a42967fb37eeaca72729271025a9e2',
//         '0x4774f6d3b3d08b5ec00115f0e2fddb92604b39e52b0dc908c6f8fcb7aa5d2a9a'
//       ],
//       transactionHash: '0x5b73e239c55d790e3c9c3bbb84092652db01bb8dbf49ccc9e4a318470419d9a0',
//       transactionIndex: 315
//     },
//     {
//       address: '0x00000000000C2E074eC69A0dFb2997BA6C7d2e1e',
//       blockHash: '0x8a179bc6cb299f936c4fd614995e62d597ec6108b579c23034fb220967ceaa94',
//       blockNumber: 12598244,
//       data: '0x000000000000000000000000a2c122be93b0074270ebee7f6b7292c7deb45047',
//       logIndex: 161,
//       topics: [
//         '0x335721b01866dc23fbee8b6b2c7b1e14d6f05c28cd35a2c934239f94095602a0',
//         '0x790fdce97f7b2b1c4c5a709fb6a49bf878feffcaa85ed0245f6dff09abcefda7'
//       ],
//       transactionHash: '0x5b73e239c55d790e3c9c3bbb84092652db01bb8dbf49ccc9e4a318470419d9a0',
//       transactionIndex: 315
//     }
//   ],
//   logsBloom: '0x00000000000000000000000000000000000000000000000000000000000000000800000000000000000000000000004000000000000010000000000000020000000000000000000040000000000000000000000000000000000000000000000000000000000000000000001000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000000000000040000000000000000100004000000000000008000040000000000000000000000000000000000005000000000041000000000000000000000000000000000000000000000000100000000000000001000000000000000000000',
//   status: 1,
//   to: null,
//   transactionHash: '0x5b73e239c55d790e3c9c3bbb84092652db01bb8dbf49ccc9e4a318470419d9a0',
//   transactionIndex: 315,
//   type: 0
// }
```

#### *provider* . **sendTransaction**( transaction ) => *Promise< [TransactionResponse](/v5/api/providers/types/#providers-TransactionResponse) >*

Submits *transaction* to the network to be mined. The *transaction* **must** be signed, and be valid (i.e. the nonce is correct and the account has sufficient balance to pay for the transaction).


```javascript
const signedTx = "0x02f874827a6904849502f900849502f910825209945555763613a12d8f3e73be831dff8598089d3dca882b992b75cbeb600080c001a078dc7c068d79ecf6f3fdf003997bcba2ccd4b5eb5f59acc4d5d4ac0a33f0cd99a054c0dedfb15010cb761c41bee9280d437abef28b0292cf13fd41000519a3a9ee";
await provider.sendTransaction(signedTx);
// {
//   accessList: [],
//   chainId: 31337,
//   confirmations: 0,
//   data: '0x',
//   from: '0x2143AF6436D9Ff82b5327Fc94066a522b9CFac20',
//   gasLimit: { BigNumber: "21001" },
//   gasPrice: null,
//   hash: '0x1764f2cfd83d84c4b0136d0f69fe7cfeeb4af14f0147555d37c966911bfcb2ca',
//   maxFeePerGas: { BigNumber: "2500000016" },
//   maxPriorityFeePerGas: { BigNumber: "2500000000" },
//   nonce: 4,
//   r: '0x78dc7c068d79ecf6f3fdf003997bcba2ccd4b5eb5f59acc4d5d4ac0a33f0cd99',
//   s: '0x54c0dedfb15010cb761c41bee9280d437abef28b0292cf13fd41000519a3a9ee',
//   to: '0x5555763613a12D8F3e73be831DFf8598089d3dCa',
//   type: 2,
//   v: 1,
//   value: { BigNumber: "3141590000000000000" },
//   wait: [Function]
// }
```

#### *provider* . **waitForTransaction**( hash [ , confirms = 1 [ , timeout ] ] ) => *Promise< [TxReceipt](/v5/api/providers/types/#providers-TransactionReceipt) >*

Returns a Promise which will not resolve until *transactionHash* is mined.

If *confirms* is 0, this method is non-blocking and if the transaction has not been mined returns null. Otherwise, this method will block until the transaction has *confirms* blocks mined on top of the block in which is was mined.


Event Emitter Methods
---------------------

#### *provider* . **on**( eventName , listener ) => *this*

Add a *listener* to be triggered for each *eventName* [event](/v5/api/providers/provider/#Provider--events).


#### *provider* . **once**( eventName , listener ) => *this*

Add a *listener* to be triggered for only the next *eventName* [event](/v5/api/providers/provider/#Provider--events), at which time it will be removed.


#### *provider* . **emit**( eventName , ...args ) => *boolean*

Notify all listeners of the *eventName* [event](/v5/api/providers/provider/#Provider--events), passing *args* to each listener. This is generally only used internally.


#### *provider* . **off**( eventName [ , listener ] ) => *this*

Remove a *listener* for the *eventName* [event](/v5/api/providers/provider/#Provider--events). If no *listener* is provided, all listeners for *eventName* are removed.


#### *provider* . **removeAllListeners**( [ eventName ] ) => *this*

Remove all the listeners for the *eventName* [events](/v5/api/providers/provider/#Provider--events). If no *eventName* is provided, **all** events are removed.


#### *provider* . **listenerCount**( [ eventName ] ) => *number*

Returns the number of listeners for the *eventName* [events](/v5/api/providers/provider/#Provider--events). If no *eventName* is provided, the total number of listeners is returned.


#### *provider* . **listeners**( eventName ) => *Array< Listener >*

Returns the list of Listeners for the *eventName* [events](/v5/api/providers/provider/#Provider--events).


### Events

#### **Log Filter**

A filter is an object, representing a contract log Filter, which has the optional properties `address` (the source contract) and `topics` (a topic-set to match).

If `address` is unspecified, the filter matches any contract address.

See [EventFilters](/v5/api/providers/types/#providers-EventFilter) for more information on filtering events.


#### **Topic-Set Filter**

The value of a **Topic-Set Filter** is a array of Topic-Sets.

This event is identical to a *Log Filter* with the address omitted (i.e. from any contract).

See [EventFilters](/v5/api/providers/types/#providers-EventFilter) for more information on filtering events.


#### **Transaction Filter**

The value of a **Transaction Filter** is any transaction hash.

This event is emitted on every block that is part of a chain that includes the given mined transaction. It is much more common that the [once](/v5/api/providers/provider/#Provider-once) method is used than the [on](/v5/api/providers/provider/#Provider-on) method.



In addition to transaction and filter events, there are several named events.


Named Provider Events



```javascript
provider.on("block", (blockNumber) => {
    // Emitted on every block change
})


provider.once(txHash, (transaction) => {
    // Emitted when the transaction has been mined
})


// This filter could also be generated with the Contract or
// Interface API. If address is not specified, any address
// matches and if topics is not specified, any log matches
filter = {
    address: "dai.tokens.ethers.eth",
    topics: [
        utils.id("Transfer(address,address,uint256)")
    ]
}
provider.on(filter, (log, event) => {
    // Emitted whenever a DAI token transfer occurs
})


// Notice this is an array of topic-sets and is identical to
// using a filter with no address (i.e. match any address)
topicSets = [
    utils.id("Transfer(address,address,uint256)"),
    null,
    [
        hexZeroPad(myAddress, 32),
        hexZeroPad(myOtherAddress, 32)
    ]
]
provider.on(topicSets, (log, event) => {
    // Emitted any token is sent TO either address
})


provider.on("pending", (tx) => {
    // Emitted when any new pending transaction is noticed
});


provider.on("error", (tx) => {
    // Emitted when any error occurs
});
```

Inspection Methods
------------------

#### *Provider* . **isProvider**( object ) => *boolean*

Returns true if and only if *object* is a Provider.


