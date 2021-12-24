-----

Documentation: [html](https://docs.ethers.io/)

-----

Encoding Utilities
==================

Base58
------

#### *ethers* . *utils* . *base58* . **decode**( textData ) => *Uint8Array*

Return a typed Uint8Array representation of *textData* decoded using base-58 encoding.


```javascript
base58.decode("TzMhH");
// Uint8Array [ 18, 52, 86, 120 ]
```

#### *ethers* . *utils* . *base58* . **encode**( aBytesLike ) => *string*

Return *aBytesLike* encoded as a string using the base-58 encoding.


```javascript
base58.encode("0x12345678");
// 'TzMhH'

base58.encode([ 0x12, 0x34, 0x56, 0x78 ]);
// 'TzMhH'
```

Base64
------

#### *ethers* . *utils* . *base64* . **decode**( textData ) => *Uint8Array*

Return a typed Uint8Array representation of *textData* decoded using base-64 encoding.


```javascript
base64.decode("EjQ=");
// Uint8Array [ 18, 52 ]
```

#### *ethers* . *utils* . *base64* . **encode**( aBytesLike ) => *string*

Return *aBytesLike* encoded as a string using the base-64 encoding.


```javascript
base64.encode("0x1234");
// 'EjQ='

base64.encode([ 0x12, 0x34 ]);
// 'EjQ='
```

Recursive-Length Prefix
-----------------------

#### *ethers* . *utils* . *RLP* . **encode**( dataObject ) => *string< [DataHexString](/v5/api/utils/bytes/#DataHexString) >*

Encode a structured [Data Object](/v5/api/utils/encoding/#rlp--dataobject) into its RLP-encoded representation.


```javascript
RLP.encode("0x12345678");
// '0x8412345678'

RLP.encode([ "0x12345678" ]);
// '0xc58412345678'

RLP.encode([ new Uint8Array([ 0x12, 0x34, 0x56, 0x78 ]) ]);
// '0xc58412345678'

RLP.encode([ [ "0x42", [ "0x43" ] ], "0x12345678", [ ] ]);
// '0xcac342c1438412345678c0'

RLP.encode([ ]);
// '0xc0'
```

#### *ethers* . *utils* . *RLP* . **decode**( aBytesLike ) => *[DataObject](/v5/api/utils/encoding/#rlp--dataobject)*

Decode an RLP-encoded *aBytesLike* into its structured [Data Object](/v5/api/utils/encoding/#rlp--dataobject).

All Data components will be returned as a [DataHexString](/v5/api/utils/bytes/#DataHexString).


```javascript
RLP.decode("0x8412345678");
// '0x12345678'

RLP.decode("0xcac342c1438412345678c0");
// [
//   [
//     '0x42',
//     [
//       '0x43'
//     ]
//   ],
//   '0x12345678',
//   []
// ]

RLP.decode("0xc0");
// []
```

### Data Object

#### **Examples**

- `"0x1234"` 
- `[ "0x1234", [ "0xdead", "0xbeef" ], [ ] ]` 




