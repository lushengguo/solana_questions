solana_questions

- solana的'矿工‘是如何'挖矿'的?
https://docs.anza.xyz/consensus/leader-rotation
简单来说就是一堆挖矿的节点(其实这里已经没有挖矿的概念了, 这些全节点统称为regular node or validator)通过共识算法, 
在下一段时间内(术语叫epoch, 目前来说是两天), 有一个leader schedule, 里面是下一届leader list,
用round robin的方式轮流当领导/生成区块, 每人负责一个slot,
这个leader schedule是写在block里的, 在下个epoch开始之前, 计算出来下一个leader schedule

- 看到POH机制解决了区块链的分叉问题, 真的解决了吗? 怎么解决的?
目前看下来选举leader schdule的时候有点关系, 因为每个slot都是有对应的负责人的, 没生成区块或者做恶生成了无效区块, 
都不会被validator接受.

FYI:
# Leader Schedule Generation Algorithm
Leader schedule is generated using a predefined seed. The process is as follows:

1. Periodically use the PoH tick height (a monotonically increasing counter) to seed a stable pseudo-random algorithm.
2. At that height, sample the bank for all the staked accounts with leader identities that 
   have voted within a cluster-configured number of ticks. The sample is called the active set.
3. Sort the active set by stake weight.
4. Use the random seed to select nodes weighted by stake to create a stake-weighted ordering.
5. This ordering becomes valid after a cluster-configured number of ticks.


- POH存在的必要性是什么, 它跟solana支持每秒大量tx有关吗?
