# B-Tree
## 结构性质
阶为M的B树：
* 根要么是叶节点，要么其具有2到M个子节点
* 除根外，所有非叶节点的子节点数量在[M/2]和M之间
* 叶节点中关键字的个数也在[M/2]和M之间
* 所有叶节点都在相同的深度上， 且具有
* 所有的数据都存储在叶节点上（另一种流行的定义允许关键字储存在内部节点上）（**叶节点上储存的关键字有序**）
* 对于每一个节点，其子树Pk中所有的关键字都小于子树Pk+1中的关键字
* 每个内部节点上，除了储存着指向各子节点的指针P1,P2...Pm,还**储存着子树P2,P3...Pm上最小的关键字**k1,k2......km-1。  
4阶B-树常叫做2-3-4树，3阶B-树常叫做2-3树  
* B-树的最大深度为[log[M/2]N]

## 基本操作
### Find
通过与储存在内部节点上的*各子树的最小关键字*比较，在M(可能不足M)个子树中确定一个子树，进一步查找
### FindMin/FindMax
### Insert⭐

### Delete


* Insert和Delete的从时间角度来说，M的最好选择是3或4，M再增大时插入和删除的时间就会增加。

### 应用：
用于对磁盘的访问，协调较慢的磁盘读取与CPU的处理速度