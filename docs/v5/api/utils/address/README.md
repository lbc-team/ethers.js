-----

Documentation: [html](https://docs.ethers.io/)

-----

Addresses
=========

Address Formats
---------------

### Address

### ICAP Address

Converting and Verifying
------------------------

#### *ethers* . *utils* . **getAddress**( address ) => *string< [Address](/v5/api/utils/address/#address) >*

Returns *address* as a Checksum Address.

If *address* is an invalid 40-nibble [HexString](/v5/api/utils/bytes/#HexString) or if it contains mixed case and the checksum is invalid, an [INVALID_ARGUMENT](/v5/api/utils/logger/#errors--invalid-argument) Error is thrown.

The value of *address* may be any supported address format.


```javascript
// Injects the checksum (via upper-casing specific letters)
getAddress("0x8ba1f109551bd432803012645ac136ddd64dba72");
// '0x8ba1f109551bD432803012645Ac136ddd64DBA72'

// Converts and injects the checksum
getAddress("XE65GB6LDNXYOFTX0NSV3FUWKOWIXAMJK36");
// '0x8ba1f109551bD432803012645Ac136ddd64DBA72'

// Throws if a checksummed address is provided, but a
// letter is the wrong case
// ------------v (should be lower-case)
getAddress("0x8Ba1f109551bD432803012645Ac136ddd64DBA72")
// [Error: bad address checksum] {
//   argument: 'address',
//   code: 'INVALID_ARGUMENT',
//   reason: 'bad address checksum',
//   value: '0x8Ba1f109551bD432803012645Ac136ddd64DBA72'
// }

// Throws if the ICAP/IBAN checksum fails
getIcapAddress("XE65GB6LDNXYOFTX0NSV3FUWKOWIXAMJK37");
// Error: getIcapAddress is not defined

// Throws if the address is invalid, in general
getIcapAddress("I like turtles!");
// Error: getIcapAddress is not defined
```

#### *ethers* . *utils* . **getIcapAddress**( address ) => *string< [IcapAddress](/v5/api/utils/address/#address-icap) >*

Returns *address* as an [ICAP address](https://github.com/ethereum/wiki/wiki/Inter-exchange-Client-Address-Protocol-%28ICAP%29). Supports the same restrictions as [getAddress](/v5/api/utils/address/#utils-getAddress).


```javascript
getIcapAddress("0x8ba1f109551bd432803012645ac136ddd64dba72");
// 'XE65GB6LDNXYOFTX0NSV3FUWKOWIXAMJK36'

getIcapAddress("XE65GB6LDNXYOFTX0NSV3FUWKOWIXAMJK36");
// 'XE65GB6LDNXYOFTX0NSV3FUWKOWIXAMJK36'
```

#### *ethers* . *utils* . **isAddress**( address ) => *boolean*

Returns true if *address* is valid (in any supported format).


```javascript
isAddress("0x8ba1f109551bd432803012645ac136ddd64dba72");
// true

isAddress("XE65GB6LDNXYOFTX0NSV3FUWKOWIXAMJK36");
// true

isAddress("I like turtles.");
// false
```

Derivation
----------

#### *ethers* . *utils* . **computeAddress**( publicOrPrivateKey ) => *string< [Address](/v5/api/utils/address/#address) >*

Returns the address for *publicOrPrivateKey*. A public key may be compressed or uncompressed, and a private key will be converted automatically to a public key for the derivation.


```javascript
// Private Key
computeAddress("0xb976778317b23a1385ec2d483eda6904d9319135b89f1d8eee9f6d2593e2665d");
// '0x0Ac1dF02185025F65202660F8167210A80dD5086'

// Public Key (compressed)
computeAddress("0x0376698beebe8ee5c74d8cc50ab84ac301ee8f10af6f28d0ffd6adf4d6d3b9b762");
// '0x0Ac1dF02185025F65202660F8167210A80dD5086'

// Public Key (uncompressed)
computeAddress("0x0476698beebe8ee5c74d8cc50ab84ac301ee8f10af6f28d0ffd6adf4d6d3b9b762d46ca56d3dad2ce13213a6f42278dabbb53259f2d92681ea6a0b98197a719be3");
// '0x0Ac1dF02185025F65202660F8167210A80dD5086'
```

#### *ethers* . *utils* . **recoverAddress**( digest , signature ) => *string< [Address](/v5/api/utils/address/#address) >*

Use [ECDSA Public Key Recovery](https://en.wikipedia.org/wiki/Elliptic_Curve_Digital_Signature_Algorithm#Public_key_recovery) to determine the address that signed *digest* to which generated *signature*.


```javascript
const digest = "0x7c5ea36004851c764c44143b1dcb59679b11c9a68e5f41497f6cf3d480715331";

// Using an expanded Signature
recoverAddress(digest, {
  r: "0x528459e4aec8934dc2ee94c4f3265cf6ce00d47cf42bb106afda3642c72e25eb",
  s: "0x42544137118256121502784e5a6425e6183ca964421ecd577db6c66ba9bccdcf",
  v: 27
});
// '0x0Ac1dF02185025F65202660F8167210A80dD5086'

// Using a flat Signature
const signature = "0x528459e4aec8934dc2ee94c4f3265cf6ce00d47cf42bb106afda3642c72e25eb42544137118256121502784e5a6425e6183ca964421ecd577db6c66ba9bccdcf1b";
recoverAddress(digest, signature);
// '0x0Ac1dF02185025F65202660F8167210A80dD5086'
```

Contracts Addresses
-------------------

#### *ethers* . *utils* . **getContractAddress**( transaction ) => *string< [Address](/v5/api/utils/address/#address) >*

Returns the contract address that would result if *transaction* was used to deploy a contract.


```javascript
const from = "0x8ba1f109551bD432803012645Ac136ddd64DBA72";
const nonce = 5;

getContractAddress({ from, nonce });
// '0x082B6aC9e47d7D83ea3FaBbD1eC7DAba9D687b36'
```

#### *ethers* . *utils* . **getCreate2Address**( from , salt , initCodeHash ) => *string< [Address](/v5/api/utils/address/#address) >*

Returns the contract address that would result from the given [CREATE2](https://eips.ethereum.org/EIPS/eip-1014) call.


```javascript
const from = "0x8ba1f109551bD432803012645Ac136ddd64DBA72";
const salt = "0x7c5ea36004851c764c44143b1dcb59679b11c9a68e5f41497f6cf3d480715331";
const initCode = "0x6394198df16000526103ff60206004601c335afa6040516060f3";
const initCodeHash = keccak256(initCode);

getCreate2Address(from, salt, initCodeHash);
// '0x533ae9d683B10C02EbDb05471642F85230071FC3'
```

