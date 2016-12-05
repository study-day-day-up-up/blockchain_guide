## 共识算法

实际上，要保障系统满足不同程度的一致性，往往需要通过共识算法来达成。

共识算法解决的是对某个提案（Proposal），大家达成一致意见的过程。提案的含义在分布式系统中十分宽泛，如多个事件发生的顺序、某个键对应的值、谁是领导……等等，可以认为任何需要达成一致的信息都是一个提案。

### 问题挑战
实际上，如果分布式系统中各个节点都能保证以十分强大的性能（瞬间响应、高吞吐）无故障的运行，则实现共识过程并不复杂，简单通过多播过程投票即可。

很可惜的是，现实中这样“完美”的系统并不存在，如响应请求往往存在时延、网络会发生中断、节点会发生故障、甚至存在恶意节点故意要破坏系统。

一般地，把故障（不响应）的情况称为“非拜占庭错误”，恶意响应的情况称为“拜占庭错误”（对应节点为拜占庭节点）。

### 常见算法
针对非拜占庭错误的情况，一般包括 Paxos、Raft 及其变种。

对于要能容忍拜占庭错误的情况，一般包括 PBFT 系列、PoW 系列算法等。

### 理论界限

搞学术的人都喜欢对问题先确定一个界限，那么，这个问题的最坏界限在哪里呢？很不幸，一般情况下，分布式系统的共识问题无解。

当节点之间的通信网络自身不可靠情况下，很显然，无法确保实现共识。但好在，一个设计得当的网络可以在大概率上实现可靠的通信。

然而，**即便在网络通信可靠情况下，一个可扩展的分布式系统的共识问题的下限是无解。**

这个结论，被称为 `FLP 不可能性` 原理，可以看做分布式领域的“测不准原理”。