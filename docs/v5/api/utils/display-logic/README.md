-----

Documentation: [html](https://docs.ethers.io/)

-----

Display Logic and Input
=======================

Units
-----

### Decimal Count

### Named Units





Functions
---------

### Formatting

#### *ethers* . *utils* . **commify**( value ) => *string*

Returns a string with value grouped by 3 digits, separated by `,`.


```javascript
commify("-1000.3000");
// '-1,000.3'
```

### Conversion

#### *ethers* . *utils* . **formatUnits**( value [ , unit = "ether" ] ) => *string*

Returns a string representation of *value* formatted with *unit* digits (if it is a number) or to the unit specified (if a string).


```javascript
const oneGwei = BigNumber.from("1000000000");
const oneEther = BigNumber.from("1000000000000000000");

formatUnits(oneGwei, 0);
// '1000000000'

formatUnits(oneGwei, "gwei");
// '1.0'

formatUnits(oneGwei, 9);
// '1.0'

formatUnits(oneEther);
// '1.0'

formatUnits(oneEther, 18);
// '1.0'
```

#### *ethers* . *utils* . **formatEther**( value ) => *string*

The equivalent to calling `formatUnits(value, "ether")`.


```javascript
const value = BigNumber.from("1000000000000000000");

formatEther(value);
// '1.0'
```

#### *ethers* . *utils* . **parseUnits**( value [ , unit = "ether" ] ) => *[BigNumber](/v5/api/utils/bignumber/)*

Returns a [BigNumber](/v5/api/utils/bignumber/) representation of *value*, parsed with *unit* digits (if it is a number) or from the unit specified (if a string).


```javascript
parseUnits("1.0");
// { BigNumber: "1000000000000000000" }

parseUnits("1.0", "ether");
// { BigNumber: "1000000000000000000" }

parseUnits("1.0", 18);
// { BigNumber: "1000000000000000000" }

parseUnits("121.0", "gwei");
// { BigNumber: "121000000000" }

parseUnits("121.0", 9);
// { BigNumber: "121000000000" }
```

#### *ethers* . *utils* . **parseEther**( value ) => *[BigNumber](/v5/api/utils/bignumber/)*

The equivalent to calling `parseUnits(value, "ether")`.


```javascript
parseEther("1.0");
// { BigNumber: "1000000000000000000" }

parseEther("-0.5");
// { BigNumber: "-500000000000000000" }
```

