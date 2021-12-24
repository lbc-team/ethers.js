-----

Documentation: [html](https://docs.ethers.io/)

-----

ABI Formats
===========

Human-Readable ABI
------------------

```javascript
const humanReadableAbi = [

  // Simple types
  "constructor(string symbol, string name)",
  "function transferFrom(address from, address to, uint value)",
  "function balanceOf(address owner) view returns (uint balance)",
  "event Transfer(address indexed from, address indexed to, address value)",
  "error InsufficientBalance(account owner, uint balance)",

  // Some examples with the struct type, we use the tuple keyword:
  // (note: the tuple keyword is optional, simply using additional
  //        parentheses accomplishes the same thing)
  // struct Person {
  //   string name;
  //   uint16 age;
  // }
  "function addPerson(tuple(string name, uint16 age) person)",
  "function addPeople(tuple(string name, uint16 age)[] person)",
  "function getPerson(uint id) view returns (tuple(string name, uint16 age))",

  "event PersonAdded(uint indexed id, tuple(string name, uint16 age) person)"
];
```

Solidity JSON ABI
-----------------

```javascript
const jsonAbi = `[
  {
    "type": "constructor",
    "payable": false,
    "inputs": [
      { "type": "string", "name": "symbol" },
      { "type": "string", "name": "name" }
    ]
  },
  {
    "type": "function",
    "name": "transferFrom",
    "constant": false,
    "payable": false,
    "inputs": [
      { "type": "address", "name": "from" },
      { "type": "address", "name": "to" },
      { "type": "uint256", "name": "value" }
    ],
    "outputs": [ ]
  },
  {
    "type": "function",
    "name": "balanceOf",
    "constant":true,
    "stateMutability": "view",
    "payable":false, "inputs": [
      { "type": "address", "name": "owner"}
    ],
    "outputs": [
      { "type": "uint256"}
    ]
  },
  {
    "type": "event",
    "anonymous": false,
    "name": "Transfer",
    "inputs": [
      { "type": "address", "name": "from", "indexed":true},
      { "type": "address", "name": "to", "indexed":true},
      { "type": "address", "name": "value"}
    ]
  },
  {
    "type": "error",
    "name": "InsufficientBalance",
    "inputs": [
      { "type": "account", "name": "owner"},
      { "type": "uint256", "name": "balance"}
    ]
  },
  {
    "type": "function",
    "name": "addPerson",
    "constant": false,
    "payable": false,
    "inputs": [
      {
        "type": "tuple",
        "name": "person",
        "components": [
          { "type": "string", "name": "name" },
          { "type": "uint16", "name": "age" }
        ]
      }
    ],
    "outputs": []
  },
  {
    "type": "function",
    "name": "addPeople",
    "constant": false,
    "payable": false,
    "inputs": [
      {
        "type": "tuple[]",
        "name": "person",
        "components": [
          { "type": "string", "name": "name" },
          { "type": "uint16", "name": "age" }
        ]
      }
    ],
    "outputs": []
  },
  {
    "type": "function",
    "name": "getPerson",
    "constant": true,
    "stateMutability": "view",
    "payable": false,
    "inputs": [
      { "type": "uint256", "name": "id" }
    ],
    "outputs": [
      {
        "type": "tuple",
        "components": [
          { "type": "string", "name": "name" },
          { "type": "uint16", "name": "age" }
        ]
      }
    ]
  },
  {
    "type": "event",
    "anonymous": false,
    "name": "PersonAdded",
    "inputs": [
      { "type": "uint256", "name": "id", "indexed": true },
      {
        "type": "tuple",
        "name": "person",
        "components": [
          { "type": "string", "name": "name", "indexed": false },
          { "type": "uint16", "name": "age", "indexed": false }
        ]
      }
    ]
  }
]`;
```

Solidity Object ABI
-------------------

Converting Between Formats
--------------------------

```javascript
// Using the "full" format will ensure the Result objects
// have named properties, which improves code readability
const iface = new Interface(jsonAbi);
iface.format(FormatTypes.full);
// [
//   'constructor(string symbol, string name)',
//   'function transferFrom(address from, address to, uint256 value)',
//   'function balanceOf(address owner) view returns (uint256)',
//   'event Transfer(address indexed from, address indexed to, address value)',
//   'error InsufficientBalance(account owner, uint256 balance)',
//   'function addPerson(tuple(string name, uint16 age) person)',
//   'function addPeople(tuple(string name, uint16 age)[] person)',
//   'function getPerson(uint256 id) view returns (tuple(string name, uint16 age))',
//   'event PersonAdded(uint256 indexed id, tuple(string name, uint16 age) person)'
// ]
```

```javascript
// Using the "minimal" format will save a small amount of
// space, but is generally not worth it as named properties
// on Results will not be available
const iface = new Interface(jsonAbi);
iface.format(FormatTypes.minimal);
// [
//   'constructor(string,string)',
//   'function transferFrom(address,address,uint256)',
//   'function balanceOf(address) view returns (uint256)',
//   'event Transfer(address indexed,address indexed,address)',
//   'error InsufficientBalance(account,uint256)',
//   'function addPerson(tuple(string,uint16))',
//   'function addPeople(tuple(string,uint16)[])',
//   'function getPerson(uint256) view returns (tuple(string,uint16))',
//   'event PersonAdded(uint256 indexed,tuple(string,uint16))'
// ]
```

```javascript
// Sometimes you may need to export a Human-Readable ABI to
// JSON for tools that do not have Human-Readable support

// For compactness, the JSON is kept with minimal white-space
const iface = new Interface(humanReadableAbi);
jsonAbi = iface.format(FormatTypes.json);
// '[{"type":"constructor","payable":false,"inputs":[{"type":"string","name":"symbol"},{"type":"string","name":"name"}]},{"type":"function","name":"transferFrom","constant":false,"payable":false,"inputs":[{"type":"address","name":"from"},{"type":"address","name":"to"},{"type":"uint256","name":"value"}],"outputs":[]},{"type":"function","name":"balanceOf","constant":true,"stateMutability":"view","payable":false,"inputs":[{"type":"address","name":"owner"}],"outputs":[{"type":"uint256","name":"balance"}]},{"type":"event","anonymous":false,"name":"Transfer","inputs":[{"type":"address","name":"from","indexed":true},{"type":"address","name":"to","indexed":true},{"type":"address","name":"value"}]},{"type":"error","name":"InsufficientBalance","inputs":[{"type":"account","name":"owner"},{"type":"uint256","name":"balance"}]},{"type":"function","name":"addPerson","constant":false,"payable":false,"inputs":[{"type":"tuple","name":"person","components":[{"type":"string","name":"name"},{"type":"uint16","name":"age"}]}],"outputs":[]},{"type":"function","name":"addPeople","constant":false,"payable":false,"inputs":[{"type":"tuple[]","name":"person","components":[{"type":"string","name":"name"},{"type":"uint16","name":"age"}]}],"outputs":[]},{"type":"function","name":"getPerson","constant":true,"stateMutability":"view","payable":false,"inputs":[{"type":"uint256","name":"id"}],"outputs":[{"type":"tuple","components":[{"type":"string","name":"name"},{"type":"uint16","name":"age"}]}]},{"type":"event","anonymous":false,"name":"PersonAdded","inputs":[{"type":"uint256","name":"id","indexed":true},{"type":"tuple","name":"person","components":[{"type":"string","name":"name","indexed":false},{"type":"uint16","name":"age","indexed":false}]}]}]'

// However it is easy to use JSON.parse and JSON.stringify
// with formatting parameters to assist with readability
JSON.stringify(JSON.parse(jsonAbi), null, 2);
// `[
//   {
//     "type": "constructor",
//     "payable": false,
//     "inputs": [
//       {
//         "type": "string",
//         "name": "symbol"
//       },
//       {
//         "type": "string",
//         "name": "name"
//       }
//     ]
//   },
//   {
//     "type": "function",
//     "name": "transferFrom",
//     "constant": false,
//     "payable": false,
//     "inputs": [
//       {
//         "type": "address",
//         "name": "from"
//       },
//       {
//         "type": "address",
//         "name": "to"
//       },
//       {
//         "type": "uint256",
//         "name": "value"
//       }
//     ],
//     "outputs": []
//   },
//   {
//     "type": "function",
//     "name": "balanceOf",
//     "constant": true,
//     "stateMutability": "view",
//     "payable": false,
//     "inputs": [
//       {
//         "type": "address",
//         "name": "owner"
//       }
//     ],
//     "outputs": [
//       {
//         "type": "uint256",
//         "name": "balance"
//       }
//     ]
//   },
//   {
//     "type": "event",
//     "anonymous": false,
//     "name": "Transfer",
//     "inputs": [
//       {
//         "type": "address",
//         "name": "from",
//         "indexed": true
//       },
//       {
//         "type": "address",
//         "name": "to",
//         "indexed": true
//       },
//       {
//         "type": "address",
//         "name": "value"
//       }
//     ]
//   },
//   {
//     "type": "error",
//     "name": "InsufficientBalance",
//     "inputs": [
//       {
//         "type": "account",
//         "name": "owner"
//       },
//       {
//         "type": "uint256",
//         "name": "balance"
//       }
//     ]
//   },
//   {
//     "type": "function",
//     "name": "addPerson",
//     "constant": false,
//     "payable": false,
//     "inputs": [
//       {
//         "type": "tuple",
//         "name": "person",
//         "components": [
//           {
//             "type": "string",
//             "name": "name"
//           },
//           {
//             "type": "uint16",
//             "name": "age"
//           }
//         ]
//       }
//     ],
//     "outputs": []
//   },
//   {
//     "type": "function",
//     "name": "addPeople",
//     "constant": false,
//     "payable": false,
//     "inputs": [
//       {
//         "type": "tuple[]",
//         "name": "person",
//         "components": [
//           {
//             "type": "string",
//             "name": "name"
//           },
//           {
//             "type": "uint16",
//             "name": "age"
//           }
//         ]
//       }
//     ],
//     "outputs": []
//   },
//   {
//     "type": "function",
//     "name": "getPerson",
//     "constant": true,
//     "stateMutability": "view",
//     "payable": false,
//     "inputs": [
//       {
//         "type": "uint256",
//         "name": "id"
//       }
//     ],
//     "outputs": [
//       {
//         "type": "tuple",
//         "components": [
//           {
//             "type": "string",
//             "name": "name"
//           },
//           {
//             "type": "uint16",
//             "name": "age"
//           }
//         ]
//       }
//     ]
//   },
//   {
//     "type": "event",
//     "anonymous": false,
//     "name": "PersonAdded",
//     "inputs": [
//       {
//         "type": "uint256",
//         "name": "id",
//         "indexed": true
//       },
//       {
//         "type": "tuple",
//         "name": "person",
//         "components": [
//           {
//             "type": "string",
//             "name": "name",
//             "indexed": false
//           },
//           {
//             "type": "uint16",
//             "name": "age",
//             "indexed": false
//           }
//         ]
//       }
//     ]
//   }
// ]`
```

