## security
- 使用静态类型系统来检查错误。（动态->静态？）
- 使用内置的安全功能 （内置那些安全功能？？
- 可靠的编译和环境 ？
# Scalable
- 灵活的变量类型系统
- 函数重载和继承
- 智能合约的交互



#### language influences

solidity is a curly-bracket language that has been influenced and inspired by several well-known programmer languages.

``` curly-bracket language
This syntanx orginated with BCPL,and was popularized By C.
```

#### object-oriented language

- 封装性 
- 继承性 (properties are used to store data of an object,while methods are used to manipulate the data of an object.)
- 多态性 (common )
- 抽象性 （convert real world something to computer object)

``` note
opcode最后生成是不存在版本号，只是在兼容evm上执行
```
#### solidity warnings

- as similar looking(or even identical) characters can have different code points and as such are encoded as a different byte array.

``` 
identifiers -> contracts name,function names and variable names
```

### external and view
- **external:** External functions are part of the contract interface, which means they can be called from other contracts and via transactions. External functions cannot modify the state of the contract.(则只有合约本身或其子合约才能调用它?)
- **view:** View functions are read-only functions, which means they cannot modify the state of the contract. View functions are typically used to retrieve data from the contract state.
- `external`：可以被任何合约或用户调用。`external` 函数可以被任何合约或用户调用。它们可以修改对象状态，例如修改存储数据或调用其他函数。
- `public`：只能被同一个合约中的函数调用。`public` 函数只能被同一个合约中的函数调用。它们可以修改对象状态，也可以读取对象状态。
- `private`：只能被合约的构造函数和内部函数调用。
- `view` 函数只能被同一个合约中的函数调用。它们只能读取对象状态，不能修改对象状态。
合约可以通过 `external` 函数调用其他合约的 `public` 函数或 `view` 函数。
关键词：同一个合约区别。

**限制**

`external` 函数可以被任何合约或用户调用，这意味着它们可以被恶意用户利用来攻击智能合约。在设计智能合约时，应注意 `external` 函数的安全性。
#### Gas

The **gas price** is a value set by the originator of the transaction, who has to pay `gas_price * gas` up front to the EVM executor. If some gas is left after execution, it is refunded to the transaction originator. In case of an exception that reverts changes, already used up gas is not refunded.
Gas used on Ethereum came about as a way to prevent denial-of-service (DoS) attacks on the network.?
Gas price = Gas limit(evm operation cost) * Gas price per unit ()



#### storage
storage in Ethereum is a key-value store that maps 256-bit words to 256-bit words. This means that each storage slot can store a single 32-byte value, and each storage key must also be a 32-byte value.
```
  
256-bit and 32-byte are two different ways of expressing the same amount of data. A byte is a unit of data that consists of 8 bits. A bit is a binary digit, which can be either 0 or 1. Therefore, a 256-bit value is equal to 32 bytes.

Here is a table that shows the conversion between bits and bytes:

| Bits | Bytes |
|---|---|---| 
| 8 | 1 | 
| 16 | 2 | 
| 32 | 4 |
| 64 | 8 | 
| 128 | 16 | 
| 256 | 32 |

256-bit and 32-byte are commonly used to refer to the size of data types in computer science. For example, the SHA-256 hash function produces a 256-bit hash value, which is equal to 32 bytes.

In Ethereum, storage slots are 256 bits in size. This means that each storage slot can store a single 32-byte value.
```
#### message call
Contracts can call other contracts or send Ether to non-contract accounts by the means of message calls.Message calls are similar to transactions, in that they have a source, a target, data payload, Ether, gas and return data. In fact, every transaction consists of a top-level message call which in turn can create further message calls.


#### ABI coder
The ABI coder v1 and ABI coder v2 are two different versions of the ABI coder used in Ethereum. 
The ABI coder is used to encode and decode data between smart contracts and external callers, such as wallets and other contracts.

The ABI coder is used to encode and decode data between smart contracts and external callers because it provides a consistent and machine-readable format for representing data. This is important for a number of reasons:

- **Security:** The ABI coder helps to prevent security vulnerabilities by ensuring that data is encoded and decoded correctly. For example, if data is not encoded correctly, it could be possible for an attacker to manipulate the data in order to exploit a smart contract.
- **Interoperability:** The ABI coder allows different smart contracts and external callers to interact with each other seamlessly. This is because the ABI coder provides a common way to represent data, regardless of the programming language or platform that is being used.
- **Efficiency:** The ABI coder is designed to be efficient, so that data can be encoded and decoded quickly and easily. This is important for smart contracts, which need to be able to process transactions quickly and efficiently.

Here are some specific examples of how the ABI coder is used:

- **Calling smart contract functions:**
- **Decoding smart contract events:** 
- **Encoding and decoding data for transactions:** 

Overall, the ABI coder is an important tool for enabling smart contracts to interact with the world around them. It provides a consistent and machine-readable format for representing data, which helps to improve security, interoperability, and efficiency.


The new ABI coder (v2) is able to encode and decode arbitrarily nested arrays and structs. Apart from supporting more types, it involves more extensive validation and safety checks, which may result in higher gas costs, but also heightened security. It is considered non-experimental as of Solidity 0.6.0 and it is enabled by default starting with Solidity 0.8.0. The old ABI coder can still be selected using `pragma abicoder v1;`.
The set of types supported by the new encoder is a strict superset of the ones supported by the old one. Contracts that use it can interact with ones that do not without limitations. The reverse is possible only as long as the non-`abicoder v2` contract does not try to make calls that would require decoding types only supported by the new encoder. The compiler can detect this and will issue an error. Simply enabling `abicoder v2` for your contract is enough to make the error go away.
Up to Solidity 0.7.4, it was possible to select the ABI coder v2 by using `pragma experimental ABIEncoderV2`, but it was not possible to explicitly select coder v1 because it was the default.

#### Structure of a Contract
- State Variables
- Functions
- Function Modifiers
- Events
- Error
- Struct Types
- Enum Types

### Types


The concept of “undefined” or “null” values does not exist in Solidity, but newly declared variables always have a [default value](https://docs.soliditylang.org/en/v0.8.21/control-structures.html#default-value) dependent on its type. To handle any unexpected values, you should use the [revert function](https://docs.soliditylang.org/en/v0.8.21/control-structures.html#assert-and-require) to revert the whole transaction, or return a tuple with a second `bool` value denoting success.

``` solidity
uint256 myUint256; // myUint256 == 0
string myString; // myString == ""
bool myBool; // myBool == false
address myAddress; // myAddress == 0x0000000000000000000000000000000000000000
```

#### 负数

`设计目的`
- 提供了一种方便计算负数的方法。例如，如果 `x` 是一个有符号整数，我们可以使用 `-x` 来计算它的负数，而不需要使用其他的表达式，例如 `T(0) - x`。
- 允许将有符号整数转换为无符号整数。例如，如果 `x` 是一个有符号整数，我们可以使用 `-x` 将其转换为无符号整数。
- 可以用于实现各种数学算法和数据结构。例如，我们可以使用 `-x` 来实现负数乘法和除法等运算。

Solidity 中计算负数一般用于以下方面：

- 表示金额或数量：在许多应用程序中，需要表示金额或数量，例如余额、账户余额、商品数量等。在这些情况下，负数可以用于表示负余额、负账户余额或负数量。
- 表示方向或状态：在某些情况下，负数可以用于表示方向或状态。例如，在游戏中，负数可以用于表示角色的生命值或资源。
- 表示差异或变化：负数可以用于表示差异或变化。例如，在财务应用程序中，负数可以用于表示损失或赤字。

`T(0)` 是 `T` 类型的最大值。例如，`int32(0)` 是 2147483647，`uint32(0)` 是 4294967295。
在 Solidity 中，负数是使用补码表示的。补码表示将负数表示为其相反数加上 1。例如，`-128` 的补码表示是 `10000000`。
当 `x` 是负数时，`-x` 的值可能会是正数。这是因为补码表示将负数表示为其相反数加上 1。例如，`-128` 的补码表示是 `10000000`。当我们将其从 8 位有符号整数的最大值（127）中减去时，我们得到 128。
it if an operation results in a value outside of the range of the type, the call is reverted. This helps to prevent unexpected behavior and security vulnerabilities.

int256(0) == int256(-1)

在 Solidity 中，`int256` 是 256 位有符号整数。由于有符号整数的范围是从 -2**256 到 2**256 - 1，因此 `int256(0)` 和 `int256(-1)` 是两个完全不同的值。

`int256(0)` 是 0，而 `int256(-1)` 是 -1。在 Solidity 中，负数是使用补码表示的，因此 `int256(-1)` 实际上是 2**256 - 1。

因此，`int256(0) == int256(-1)` 的值为 `false`。



The expression -x is equivalent to (T(0) - x) where T is the type of x. It can only be applied to signed types. The value of -x can be positive if x is negative. There is another caveat also resulting from two’s complement representation。
- 提供了一种方便计算负数的方法。例如，如果 `x` 是一个有符号整数，我们可以使用 `-x` 来计算它的负数，而不需要使用其他的表达式，例如 `T(0) - x`。
- 允许将有符号整数转换为无符号整数。例如，如果 `x` 是一个有符号整数，我们可以使用 `-x` 将其转换为无符号整数。
- 可以用于实现各种数学算法和数据结构。例如，我们可以使用 `-x` 来实现负数乘法和除法等运算。
#### shift
- `x << y` is equivalent to the mathematical expression `x * 2**y`.
    
- `x >> y` is equivalent to the mathematical expression `x / 2**y`, rounded towards negative infinity.

#### Addition, Subtraction and Multiplication,Divsion,modulo


#### address
- `address`: Holds a 20 byte value (size of an Ethereum address).
    
- `address payable`: Same as `address`, but with the additional members `transfer` and `send`.
Implicit conversions from `address payable` to `address` are allowed, whereas conversions from `address` to `address payable` must be explicit via `payable(<address>)`.
Explicit conversions to and from `address` are allowed for `uint160`, integer literals, `bytes20` and contract types.
If you convert a type that uses a larger byte size to an `address`, for example `bytes32`, then the `address` is truncated. To reduce conversion ambiguity, starting with version 0.4.24, the compiler will force you to make the truncation explicit in the conversion. Take for example the 32-byte value `0x111122223333444455556666777788889999AAAABBBBCCCCDDDDEEEEFFFFCCCC`.

`address(uint160(bytes20(b)))` ->  `0x111122223333444455556666777788889999aAaa`
address(uint160(uint256(b)))  ->  `0x777788889999AaAAbBbbCcccddDdeeeEfFFfCcCc`.

member of address:
- balance
- transfer
- send (`send` is the low-level counterpart of `transfer`. If the execution fails, the current contract will not stop with an exception, but `send` will return `false`.)
- call
- delegatecall
- staticcall
- code (Use `.code` to get the EVM bytecode as a `bytes memory`, which might be empty.)
- codehash (Use `.codehash` to get the Keccak-256 hash of that code (as a `bytes32`). Note that `addr.codehash` is cheaper than using `keccak256(addr.code)`)
They all take a single `bytes memory` parameter and return the success condition (as a `bool`) and the returned data (`bytes memory`). The functions `abi.encode`, `abi.encodePacked`, `abi.encodeWithSelector` and `abi.encodeWithSignature` can be used to encode structured data.


The literal `MeE` is equivalent to `M * 10**E`. Examples include `2e10`, `-2e10`, `2e-10`, `2.5e1`.
Integer literals are formed from a sequence of digits in the range 0-9.
Hexadecimal literals are prefixed with the keyword `hex` and are enclosed in double or single-quotes (`hex"001122FF"`, `hex'0011_22_FF'`).
Multiple hexadecimal literals separated by whitespace are concatenated into a single literal: `hex"00112233" hex"44556677"` is equivalent to `hex"0011223344556677"`


#### Function Type
```  solidity
function (<parameter types>) {internal|external} [pure|view|payable] [returns (<return types>)]
```

#### rereference Types
Values of reference type can be modified through multiple different names. 
Contrast this with value types where you get an independent copy whenever a variable of value type is used. 
Because of that, reference types have to be handled more carefully than value types. 
- mappings.
- structs
- arrays

If you use a reference type, you always have to explicitly provide the data area where the type is stored: 
`memory` (whose lifetime is limited to an external function call)
`storage` (the location where the state variables are stored, where the lifetime is limited to the lifetime of a contract) or 
`calldata` (special data location that contains the function arguments).

An assignment or type conversion that changes the data location will always incur an automatic copy operation, while assignments inside the same data location only copy in some cases for storage types.


### Data location and assignment behavior
`Memory is a temporary data location that stores function parameters and local variables`
`Storage is a permanent data location that stores the state of your contract.`
Data locations are not only relevant for persistency of data, but also for the semantics of assignments:

- Assignments between `storage` and `memory` (or from `calldata`) always create an independent copy.
    
- Assignments from `memory` to `memory` only create references. This means that changes to one memory variable are also visible in all other memory variables that refer to the same data.
```
Avoid assigning memory variables to other memory variables unless you are sure that you want to create a reference.
If you need to create a copy of a memory variable, you can use the `abi.decode()` function.
- Be careful when modifying memory variables that are passed as arguments to functions. Changes to these variables will be visible to the calling function.
```
- Assignments from `storage` to a **local** storage variable also only assign a reference.
    
- All other assignments to `storage` always copy. Examples for this case are assignments to state variables or to members of local variables of storage struct type, even if the local variable itself is just a reference.
### Arrays
Arrays can have a compile-time fixed size, or they can have a dynamic size.
The type of an array of fixed size `k` and element type `T` is written as `T[k]`, and an array of dynamic size as `T[]`.
`Indices are zero-based, and access is in the opposite direction of the declaration.`
Array elements can be of any type, including mapping or struct.
Dynamically-sized arrays can only be resized in storage. `In memory`, such arrays can be of arbitrary size but the size cannot be changed once an array is allocated.

Variables of type `bytes` and `string` are special arrays. The `bytes` type is similar to `bytes1[]`, but it is packed tightly in calldata and memory. `string` is equal to `bytes` but does not allow length or index access.

Solidity does not have string manipulation functions, but there are third-party string libraries. You can also compare two strings by their keccak256-hash using `keccak256(abi.encodePacked(s1)) == keccak256(abi.encodePacked(s2))` and concatenate two strings using `string.concat(s1, s2)`.

```
contract StringExample {
    string public s = "Hello, world!";

    function setSeventhByteToX() public {
        bytes(s).length / bytes(s)[7] = 'x';
    }

    function printString() public view {
        console.log(s);
    }
}

```

##### array member
- length
- push() and push (x)
- pop()
To use arrays of arrays in external (instead of public) functions, you need to activate ABI coder v2.

#### Dangling References to Storage Array Elements
 take care to avoid dangling references.
 You need to take particular care when dealing with references to elements of bytes arrays, since a .push() on a bytes array may switch from short to long layout in storage.
 ```
 short -> long
 long -> short
 ```

#### array slices
Array slices are a view on a contiguous portion of an array. They are written as x[start:end], where start and end are expressions resulting in a uint256 type (or implicitly convertible to it). The first element of the slice is x[start] and the last element is x[end - 1].
```
As of now, array slices are only implemented for calldata arrays.

```

#### struts
结构体是一种自定义的数据类型，它可以包含多个成员变量。结构体可以用于存储各种类型的数据，例如用户信息、产品信息等。

结构体可以在映射和数组中使用，并且它们本身也可以包含映射和数组。这使得结构体非常灵活，可以用于构建各种复杂的数据结构。
但是，结构体不能包含其自身类型的成员。这是因为结构体的大小必须是有限的。如果结构体包含其自身类型的成员，那么结构体的大小将是无限的，这会导致错误。

在所有函数中，结构体类型都被分配给具有存储数据位置的局部变量。这不会复制结构体，而只是存储一个引用，以便对局部变量成员的赋值实际上会写入状态。

在使用结构体时，需要注意以下几点：

结构体的大小必须是有限的。
结构体不能包含其自身类型的成员。
在函数中，结构体类型通常被分配给具有存储数据位置的局部变量。
也可以直接访问结构体的成员，而无需将其分配给局部变量。


```
Until Solidity 0.7.0, memory-structs containing members of storage-only types (e.g. mappings) were allowed and assignments like campaigns[campaignID] = Campaign(beneficiary, goal, 0, 0) in the example above would work and just silently skip those members.


```
在 Solidity 中，结构体类型可以包含两种类型的成员：存储类型成员和内存类型成员。存储类型成员的值存储在合约的存储中，内存类型成员的值存储在函数调用期间使用的内存中。

在 Solidity 0.7.0 之前，如果将一个包含存储类型成员的结构体分配给一个内存变量，那么对该内存变量的赋值操作将会忽略存储类型成员。这意味着，即使您修改了内存变量的值，存储类型成员的值也不会被更新。
如果攻击者能够控制一个包含存储类型成员的结构体，那么他们可以通过修改内存变量的值来修改存储类型成员的值。这可能导致安全漏洞。例如，假设您有一个合约，其中 balance 成员存储了用户的余额。如果攻击者能够控制一个包含 balance 成员的结构体，那么他们可以通过修改内存变量的 balance 成员来盗取用户的资金。



#### mapping type
Mapping types use the syntax mapping(KeyType KeyName? => ValueType ValueName?) and variables of mapping type are declared using the syntax mapping(KeyType KeyName? => ValueType ValueName?) VariableName.
The KeyType can be any built-in value type, bytes, string, or any contract or enum type. 

`Other user-defined or complex types, such as mappings, structs or array types are not allowed. `

ValueType can be any type, including mappings, arrays and structs. KeyName and ValueName are optional (so mapping(KeyType => ValueType) works as well) and can be any valid identifier that is not a type

### Ternary Operator
The ternary operator in Solidity is a `conditional` operator that takes three operands: a `condition`, an expression to execute if the condition is true, and an expression to execute if the condition is false.

condition ? expression1 : expression2

### compound and Increment/Decrement Operators

- a+=e a=a+e
- a++ and a-- are equivalent to a += 1 / a -= 1


### delete

- delete a = a = 0;
- delete a[x];
- delete struts
- delete mapping
这是因为 delete 操作符无法知道映射 myMapping 中的键为 1 的元素存储在哪个存储槽中。因此，delete 操作符对映射没有影响。
如果要删除映射中的元素，可以使用 mapping.remove() 函数。mapping.remove() 函数会从映射中删除指定的键和值。

如果删除一个 struct，则会重置所有非mapping，并递归遍历成员（除非它们是映射）。但是，可以删除单个键及其映射到的值：如果 a 是一个映射，则 delete a[x] 将删除存储在 x 处的值。

