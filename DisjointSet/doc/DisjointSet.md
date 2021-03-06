# Disjoint Set 不相交集
* 等价关系 equivalence relation：满足自反性、对称性、传递性的关系
* 等价类 equivalence class：a∈S，S中所有于a有关系的元素的集合。
    * 等价类形成对S的划分
    * 为验证a于b是否有关系，只需验证a和b是否在一个等价类中

## 结构
* 用1-N的编号代替元素（编号可由散列等建立）。
* 由树结构表示集合，集合的名字由根节点指出。
* 节点仅储存其父节点的指针即可。
* 用数组P来储存这些树，P[i] 表示元素i的父节点（i为元素的编号 1≤i≤N）。
* 如果i是根节点
    * P[i] 可以是 0 
    * P[i] 可以是 大小(树中节点的个数)的**负数** （以区分根与普通节点）， 以实现*按大小求并(union-by-size)*
    * P[i] 可以是 树的高度的**负数**，以实现按 *高度求并(union-by-height)*

## 基本操作：
Union/Find算法：
### Find
* 返回包含给定元素的等价类的名字。
* 路径压缩(path compression):Find(X)时，从X到根的路径上的每一个节点都使它的父节点变成根。与按大小求并完全兼容。
    * 采用路径压缩时，连续M次操作最多需O(M logN)的时间。
### Union
把两个不在同一个等价类中的a与b的等价类合并成一个新的等价类。
* 按大小求并（union-by-size）让较小的树称为较大的树的子树->任何节点的深度均不会超过logN
* 按高度求并（union-by-height）让较矮的树称为较高的树的子树（只有当两颗**高度相等**的树求并时，树的高度才增加。）->任何节点的深度均不会超过logN

### 判断两个元素是否存在关系: Find(a) == Find(b)

### M次连续的Union/Find的时间为O(M log*N)
* log*N = M <-> N = 2^2^2^2....2(平方M次)