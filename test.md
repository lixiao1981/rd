## 基本概念
Blockchain finality is the assurance or guarantee that a blockchain transaction cannot be reversed or altered. It is a critical property of blockchains, as it ensures the security and immutability of the ledger.
在区块链上，交易被认为是最终的，但仍然存在被逆转的可能性。这种可能性随着时间的推移而减小，但永远不会完全消失。概率最终性的典型例子是比特币。在比特币网络上，一个交易被认为是最终的，如果它已经被包含在至少6个区块中。但是，仍然存在一个理论上的可能性，即如果攻击者控制了比特币网络的51%以上的算力，他们可以逆转任何6个区块之前的交易。
概率最终性的判断标准：
- 所需的交易安全级别
- 交易吞吐量的需求
- 成本
如果对交易安全性要求很高，则应选择使用确定性最终性的区块链，例如以太坊。
如果对交易吞吐量要求很高，则应选择使用概率最终性的区块链，例如比特币。
## two main types of blockchain finality
### Deterministic finality
In a blockchain with deterministic finality, once a transaction is added to a block, it is irreversible. This is achieved by using a consensus mechanism that ensures that all nodes in the network agree on the order of blocks. Bitcoin and Ethereum are examples of blockchains with deterministic finality.  

### Probabilistic finality 
In a blockchain with probabilistic finality, transactions are considered to be finalized after a certain period of time. This is because it is possible for a malicious actor to reverse a transaction if they control a majority of the network’s hashpower. However, the probability of this happening decreases over time, as the attacker would need to control more and more hashpower to reverse older blocks. Algorand and Solana are examples of blockchains with probabilistic finality.




### 延迟最终性
以太坊 PoS（Casper FFG）：Casper FFG 是正在为以太坊 2.0 开发的共识机制。它是一种概率最终性机制，这意味着在交易被包含在区块中后，仍有小概率被逆转。
波卡（GRANDPA）：GRANDPA 是波卡使用的共识机制。它是一种拜占庭容错（BFT）共识机制，这意味着它非常难以攻击。但是，它确实具有一些延迟最终性，因为网络需要一些时间才能就链的状态达成共识。
Solana：Solana 是一个使用证明历史（PoH）共识机制的区块链。PoH 是一种概率最终性机制，这意味着在交易被包含在区块中后，仍有小概率被逆转。

### 即时最终性
Cosmos：Cosmos 是一个使用 Tendermint BFT 共识机制的区块链。Tendermint BFT 是一种 BFT 共识机制，这意味着它非常难以攻击。它还具有即时最终性，这意味着交易在被包含在区块中后即被视为最终的。
Celestia：Celestia 是一个使用递归拜占庭容错（rBFT）共识机制的区块链。rBFT 是一种 BFT 共识机制，旨在可扩展和高效。它还具有即时最终性，这意味着交易在被包含在区块中后即被视为最终的。
Algorand：Algorand 是一个使用纯粹的证明权益（PoS）共识机制的区块链。PoS 是一种共识机制，旨在比工作量证明（PoW）更节能。它还具有即时最终性，这意味着交易在被包含在区块中后即被视为最终的。
Aptos：Aptos 是一个由 Diem 协会开发的区块链。它使用 BFT 共识机制，旨在可扩展和高效。它还具有即时最终性，这意味着交易在被包含在区块中后即被视为最终的。

## Here are some of the factors that affect blockchain finality


`The consensus mechanism`: The consensus mechanism is the process used to reach agreement on the order of blocks in the blockchain. Different consensus mechanisms have different implications for finality. For example, Nakamoto consensus, which is used by Bitcoin, is a probabilistic finality mechanism.  
`The network topology`: The network topology refers to the way in which nodes in the blockchain network are connected. A more decentralized network is more resistant to attacks, and therefore can achieve finality more quickly.  
`The block time`: The block time is the average time it takes to add a new block to the blockchain. A shorter block time can lead to faster finality, but it can also make the blockchain more vulnerable to attacks.
`the application`:

##   最终性的影响
如果一个中心化交易所或桥接网络索引了一个尚未最终确定的存款交易，那么它将面临攻击者通过导致区块链重组而进行双花攻击的风险。
## 解决方法
中心化交易所和桥接网络可以采取以下几项措施来减轻双花攻击的风险：
在索引存款交易之前等待一定数量的区块被开采。开采的区块越多，攻击者就越不可能撤销交易。  
使用具有确定性最终性的区块链。这将完全消除双花攻击的风险。  
使用具有强大共识机制的区块链。强大的共识机制将使攻击者更难撤销交易。

## security for blockchain finality

在大多数概率最终链中，用于确定规范链的叉选择规则是基于拥有最多区块的链，也称为中本聪共识。在中本聪共识下，如果网络中广播了一条更长的链，则链可能会重组，即使该链排除了之前已包含在较短链中的区块/交易。
这意味着，如果攻击者能够控制网络中超过50%的算力，他们可以创建一个比合法链更长的链。如果该链被广播到网络中，则其他节点将切换到该链，即使它排除了之前已包含在较短链中的区块/交易。
重组的风险是概率最终性的一个挑战。但是，随着链变得更长，重组的风险会随着时间而减小。这是因为攻击者越来越难以创建比合法链更长的链。
51% 重组攻击是针对概率性工作量证明网络的典型攻击。攻击者必须控制网络中超过 50% 的算力，才能创建比合法链更长的链。如果该链被广播到网络中，则其他节点将切换到该链，即使它排除了之前已包含在较短链中的区块/交易。
在这种攻击中，攻击者首先会将资金存入交易所或桥接网络。然后，他们会创建一个比合法链更长的链，该链包含一个交易，将这些资金发送给自己。如果该链被广播到网络中，则其他节点将切换到该链，并将攻击者的交易视为有效。

#### 解决反办法

在考虑交易最终之前等待一定数量的区块被开采： 开采的区块越多，发生重组的可能性就越小。
使用具有强大共识机制的区块链： 强大的共识机制，例如PoS（权益证明），可以使攻击者更难创建更长的链。
使用具有快速区块时间的区块链： 快速的区块时间也可以帮助减轻重组的风险，因为攻击者将更难在下一个区块被开采之前创建更长的链。
通过采取这些预防措施，可以降低重组的风险并提高概率最终链的最终性。
51% 重组攻击很难成功，因为需要控制网络中大量的算力。但是，如果攻击者能够成功，他们将能够控制该网络并进行各种攻击，包括双花攻击。

可以采取以下几项措施来减轻 51% 重组攻击的风险：

使用具有强大共识机制的区块链： 强大的共识机制，例如 PoS（权益证明），可以使攻击者更难创建更长的链。
使用具有快速区块时间的区块链： 快速的区块时间也可以帮助减轻重组的风险，因为攻击者将更难在下一个区块被开采之前创建更长的链。
使用分叉选择规则，该规则会考虑区块的质量和其他因素，而不是仅仅考虑区块的长度： 这种方法可以防止攻击者创建一个由无效交易组成的链。

概率最终性（Probabilistic finality）是指，在区块链上，交易被认为是最终的，但仍然存在被逆转的可能性。这种可能性随着时间的推移而减小，`但永远不会完全消失`。

概率最终性的典型例子是比特币。在比特币网络上，一个交易被认为是最终的，如果它已经被包含在至少6个区块中。但是，仍然存在一个理论上的可能性，即如果攻击者控制了比特币网络的51%以上的算力，他们可以逆转任何6个区块之前的交易。

概率最终性可以通过以下方式来衡量：

等待一定数量的区块被添加到交易之前： 等待的区块越多，发生重组的可能性就越小。
使用具有强大共识机制的区块链： 强大的共识机制，例如 Proof-of-Stake，可以使攻击者更难创建更长的链。
使用具有快速区块时间的区块链： 快速的区块时间也可以帮助减轻重组的风险，因为攻击者将更难在下一个区块被开采之前创建更长的链。

通过采取这些措施，可以提高区块链的最终性。

以下是一些常用的概率最终性度量方法：

安全阈值： 安全阈值是指需要等待的区块数，以确保交易最终确定。
确认度： 确认度是指交易已经被包含在多少个区块中。
重组概率： 重组概率是指发生重组的可能性。

这些度量方法可以帮助用户和开发人员了解交易最终性的程度，并采取适当的措施来保护他们的资金。

正确的区块延迟应该基于 both historical factors and economic factors，选择两者中较大的值作为应用程序的索引延迟。

历史因素包括：


该区块链的过去重组率。
该区块链的平均区块时间。
该区块链的算力分布。

经济因素包括：


交易的价值。
交易的紧迫性。
用户的风险承受能力。


通过考虑这些因素，应用程序可以选择一个区块延迟，为其用户提供最合适的安全性和性能。

例如，对于一个价值较低的交易，用户可能愿意接受更高的风险，因此可以选择一个较低的区块延迟。而对于一个价值较高或时间敏感的交易，用户可能希望等待更长时间以确保其最终确定，因此可以选择一个较高的区块延迟。

通过选择适当的区块延迟，应用程序可以为其用户提供最佳的交易体验。

离线应用程序开发人员在选择区块延迟时，应考虑以下历史因素：

```
链的重组率： 这是在给定时间内链被重组或恢复到早期状态的次数。重组率越高，表明链越容易受到攻击，需要更长的区块延迟来确保最终性。
重组的规模： 这是在单次重组中被逆转的区块数。重组规模越大，表明攻击者对网络的控制力越大，需要更长的区块延迟来防止双重支付攻击。
区块生产率： 这是挖出新区块的平均时间。较慢的区块生产率意味着攻击者重组链的机会较少，因此可以使用较短的区块延迟。
```

如果区块生产是概率性的，例如在工作量证明网络中，则应使用更长的区块延迟来补偿在异常短的时间内创建多个区块的可能性。这是因为较长的区块延迟将使攻击者重组链并双重支付资金变得更加困难。

通过考虑这些历史因素，离线应用程序开发人员可以选择适合其需求且能保护用户免受攻击的区块延迟。

以下是一些额外的说明：

```
所谓“重组”，是指区块链上交易记录被逆转的行为。
“双重支付攻击”是指攻击者利用区块链的最终性不确定性，重复支付相同的资金。
工作量证明（PoW）是区块链系统中一种常见的共识机制，要求参与者通过解决复杂的数学问题来获得记账权。
```

我希望这对您有所帮助！

好的，以下是翻译：

延迟最终性示例：以太坊 PoS（Casper FFG）、波卡（GRANDPA）、Solana

即时最终性示例：Cosmos、Celestia、Algorand、Aptos

你说得对。以下是一些具有延迟最终性和即时最终性的区块链示例：

延迟最终性

```
以太坊 PoS（Casper FFG）：Casper FFG 是正在为以太坊 2.0 开发的共识机制。它是一种概率最终性机制，这意味着在交易被包含在区块中后，仍有小概率被逆转。
波卡（GRANDPA）：GRANDPA 是波卡使用的共识机制。它是一种拜占庭容错（BFT）共识机制，这意味着它非常难以攻击。但是，它确实具有一些延迟最终性，因为网络需要一些时间才能就链的状态达成共识。
Solana：Solana 是一个使用证明历史（PoH）共识机制的区块链。PoH 是一种概率最终性机制，这意味着在交易被包含在区块中后，仍有小概率被逆转。
```

即时最终性

```
Cosmos：Cosmos 是一个使用 Tendermint BFT 共识机制的区块链。Tendermint BFT 是一种 BFT 共识机制，这意味着它非常难以攻击。它还具有即时最终性，这意味着交易在被包含在区块中后即被视为最终的。
Celestia：Celestia 是一个使用递归拜占庭容错（rBFT）共识机制的区块链。rBFT 是一种 BFT 共识机制，旨在可扩展和高效。它还具有即时最终性，这意味着交易在被包含在区块中后即被视为最终的。
Algorand：Algorand 是一个使用纯粹的证明权益（PoS）共识机制的区块链。PoS 是一种共识机制，旨在比工作量证明（PoW）更节能。它还具有即时最终性，这意味着交易在被包含在区块中后即被视为最终的。
Aptos：Aptos 是一个由 Diem 协会开发的区块链。它使用 BFT 共识机制，旨在可扩展和高效。它还具有即时最终性，这意味着交易在被包含在区块中后即被视为最终的。
```

选择使用具有延迟最终性还是即时最终性的区块链取决于应用程序。对于需要高安全性的应用程序，如金融应用程序，使用具有延迟最终性的区块链可能是一个更好的选择。对于需要低延迟的应用程序，如游戏应用程序，使用具有即时最终性的区块链可能是一个更好的选择。  
可证明最终性有两种类型：具有即时可证明最终性的链和具有延迟可证明最终性的链。

```
**即时可证明最终性：**这意味着交易在被包含在区块中后即被视为最终的。这是通过使用设计为非常难以攻击的共识机制来实现的。
**延迟可证明最终性：**这意味着交易在一定时间后被视为最终的，例如在一定数量的区块被挖出后。这是通过使用设计为比即时可证明最终性更高效的共识机制来实现的。
```

具有即时可证明最终性的系统的一些示例包括：

```
**Algorand：**Algorand 使用一种纯粹的证明权益（PoS）共识机制，旨在非常节能和安全。Algorand 还具有即时最终性。
**Cosmos：**Cosmos 使用 Tendermint BFT 共识机制，该机制也旨在非常安全和高效。Cosmos 也具有即时最终性。
**Celestia：**Celestia 使用递归拜占庭容错（rBFT）共识机制，旨在可扩展和高效。Celestia 也具有即时最终性。
```

具有延迟可证明最终性的系统的一些示例包括：

```
**Polkadot：**Polkadot 使用 GRANDPA 共识机制，该机制旨在非常难以攻击。但是，它确实具有一些延迟最终性，因为网络需要一些时间才能就链的状态达成共识。
**Solana：**Solana 使用证明历史（PoH）共识机制，该机制旨在非常高效。但是，它确实具有一些延迟最终性，因为网络需要一些时间才能就链的状态达成共识。
```

选择使用具有即时可证明最终性的系统还是具有延迟可证明最终性的系统取决于应用程序。对于需要高安全性的应用程序，如金融应用程序，具有即时可证明最终性的系统可能是一个更好的选择。对于需要低延迟的应用程序，如游戏应用程序，具有延迟可证明最终性的系统可能是一个更好的选择。