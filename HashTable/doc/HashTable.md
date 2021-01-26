# Hash Table
## 术语：
* hashing 散列：用于以常数时间执行插入、删除和查找的技术
* hash fuction 散列函数：将关键字映射为一个作为表的索引的值
    * 关键字是整数，则可以key mod TableSize。**表的大小最好是素数，以使散列值分布均匀**
* collision 冲突：两个关键字被映射为同以值

## 基本操作：
以平均常数时间支持：
* Insert
* Find
* Delete(懒惰删除)

## 消除冲突：
### 分离链接法 Separate chaining
**将散列到同一值的所有元素储存在表中**
* 装填因子(load factor)λ为散列表中元素的个数与散列表的大小的比值
* λ也就是每个表(list)的平均长度
* 要尽量让λ接近1
### 开发定址散列法 Open addressing hashing
**如果发生冲突，就尝试选择另外的单元，直到找到空的单元位置**  
* 试选方案： 试选单元h₀(X), h₁(X),...h_i(X), 其中**h_i(X)=(Hash(X) + F(i)) mod TableSize, F(0)=0**，函数F(X)为选定的*冲突解决方*法。
* 对于开放定址散列法，随着装填因子的上升性能下降明显，**装填因子λ应小于0.5**
* 在开放定址散列表中，**不能使用标准的删除操作**。因为相应的单元可能已经引起过冲突，使元素跳过它到了另一个单元。删除一个元素，可能会使在Find的过程中无法跳转到正确位置。所以应使用**懒惰删除**。（在插入元素的过程中可以覆盖掉被懒惰删除的元素）。
* 三个常用的冲突解决方法：
    * 线性探测法：F(i) = i。
        * 该单元不为空就找下一个。
        * 插入的元素容易聚集形成一些区块，其结果被称为*一次聚集(primary clustering)*
        * 预期插入次数对于插入和不成功的查找来说大约为(1 + 1/(1-λ)²)/2. 对于成功的查找来说大约为(1+1/(1-λ))/2.
    * 平方探测法：F(i) = i²
        * 如果表的大小为素数，那么当表至少有一半是空的时候，总能够插入一个新元素->即前⌈TableSize/2⌉ 个备选位置是互异的。
        * 表的大小是素数非常重要，若不是素数，则备选单元的数量会锐减。
        * 如果表的大小是形如4k+3的素数，且使用的平方探测法为F(i) = ±i²，那么整个表均可被探测到。
        * 优化：F(i)=i²的计算可由递推公式来加速：F(i) = F(i-1) + 2i - 1
        * 散列到同一位置的元素将探测相同的位置->二次聚集（secondary clustering）
    * 双散列(double hashing)： F(i) = i*Hash₂(X)
        * Hash₂一定不要得出0，这样是无效的
        * 一种选择：Hash₂(X)=R - (X mod R)

## 再散列 Rehashing
在使用平方探测的开放定址散列法时，为避免表的元素填的太满而导致运行时间增长和Insert操作失败，可建立另外一个大约两倍的表，将旧表中的元素（未删除的））转移到新表中->该操作即为**再散列(Rehashing)**  
### 何时进行再散列：
* 表填满一半时
* 当插入失败时
* 当表达到某个装填因子时

## 可扩散列 Extendible hashing
常用于磁盘系统，以减少对磁盘的访问次数。 
P125

## 应用
* **名字（字符串）和编号的映射**->用于节点具有实际名字的图论问题等
* 编译器使用散列表来跟踪源代码中声明的变量->符号表(symbol table)