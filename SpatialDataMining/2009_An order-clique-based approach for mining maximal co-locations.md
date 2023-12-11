## 2009_An order-clique-based approach for mining maximal co-locations

### 1.提出该方法的原因及优点

- 原因：传统方法在存储同位模式与表实例时消耗较大
- 优点：
  - 空间邻居关系和大小为2频繁co-locations被压缩到扩展前缀树结构，这使得基于排序团的方法能够挖掘候选的最大co-locations和co-locations实例
  - 在计算了相应共位关系的一些特征之后，无需存储co-locations实例，这显著减少了挖掘最大共位关系所需的执行时间和空间
- 基于排序团高效的原因：
  - 树结构支持堆实例查找方案和一种有效的修剪策略，即剪枝那些子节点数小于相关值的分支，以识别表实例
  - 它不需要存储过多的表实例来识别下一级的表实例

### 2.定义

#### 2.1最大有序频繁co-location

给定一个co-location c
$$
c={f_l,...f_v}\quad l,v∈{1,2,...,n}
$$
给定
$$
f_i∈F\quad and\quad f_i∉c
$$
如果*c∪f<sub>i</sub>*是不频繁的，则称*c*为最大有序co-location

#### 2.2size-2 co-location header relationship set

example：给定一个大小为2的co-location模式*p<sub>2</sub>*={{AB},{AC},{AD},{BC},{BD},{BF},{CD},{CE},{DE}}，它的size-2 co-location header relationship set为*δ*={*δ<sub>A</sub>*:{ABCD},*δ<sub>B</sub>*:{BCDF},*δ<sub>C</sub>*:{CDE},*δ<sub>D</sub>:{DE}}

#### 2.3size-2 colocation header relationship tree (P2-tree)

<img src="./img/2009_An%20order-clique-based%20approach%20for%20mining%20maximal%20co-locations/image-20231207095554314.png" alt="image-20231207095554314" style="zoom:80%;" />

#### 2.4特征x的排序邻近关系集合

例如：δ<sub>A</sub>={{A.1,B.1C.1},{A.2,B.4,C.2},{A.3,B.3,C.1,C.3,D.1},{A.4,B.3}}

<img src="./img/2009_An%20order-clique-based%20approach%20for%20mining%20maximal%20co-locations/image-20231207134305996.png" alt="image-20231207134305996" style="zoom:67%;" />

#### 2.5邻近关系树

以上图为例，上图的邻近关系树如下：

<img src="./img/2009_An%20order-clique-based%20approach%20for%20mining%20maximal%20co-locations/image-20231207135437404.png" alt="image-20231207135437404" style="zoom: 80%;" />

#### 2.5表实例树

以Ins作为根节点，每个分支代表了候选模式c的一个表实例的树叫做c的表实例树

基于上图计算的到的候选极大co-location模式{A,B,C}的Ins树如下图所示

![image-20231207140036902](./img/2009_An%20order-clique-based%20approach%20for%20mining%20maximal%20co-locations/image-20231207140036902.png)

生成过程可参考如下：

<img src="./img/2009_An%20order-clique-based%20approach%20for%20mining%20maximal%20co-locations/image-20231207145421856.png" alt="image-20231207145421856" style="zoom:67%;" />

#### 2.1CPI-tree设计

1. 生成CPI-tree的根，标记为null
2. 将所有空间实例按字母和数字降序弹入一个堆栈T1
3. 从堆栈T1弹出一个实例，生成根“null”的子节点，然后将这个实例推入堆栈T2
4. 从堆栈T2弹出一个实例。找出与这个实例有邻近关系的所有实例，这些实例与这个实例的空间特征不同，并且序“大于”这个实例。从堆栈T1和T2删除所有这些邻近实例，最后，将这些实例连接到CPI-tree中的相同实例（除了叶子节点）的结点上
5. 将子节点实例按降序推入堆栈T2，然后转入步骤4
6. 重复以上步骤直到堆栈T2为空，然后转入步骤3
7. 重复以上步骤知道堆栈T1为空

<img src="E:/jobfile/DataMining/notes/img/%25E6%2595%25B0%25E6%258D%25AE%25E6%258C%2596%25E6%258E%2598%25E8%25AF%25BB%25E6%2595%25B0%25E7%25AC%2594%25E8%25AE%25B013/afdc0cba26eeb315d8c348859e044f9.jpg" alt="afdc0cba26eeb315d8c348859e044f9" style="zoom: 25%;" />

### 3.用CPI-tree生成co-location表实例

#### 3.1相关概念和性质

定义：

- 直接孩子链direct-child-link：CPI-tree中两个结点之间的链接称为直接孩子链。一个长度为k的直接孩子链称为k阶直接孩子链。位于k阶直接孩子链中间的结点称为内部结点

- 间接孩子链indirect-child-link：用虚线链接的孩子结点称为间接孩子

- 全链all-link：如果k阶直接孩子链的每个内部结点的所有孩子结点是对应内部结点的兄弟，则k阶直接孩子链称为k阶全链，为方便理解参考下图

  <img src="E:/jobfile/DataMining/notes/img/%25E6%2595%25B0%25E6%258D%25AE%25E6%258C%2596%25E6%258E%2598%25E8%25AF%25BB%25E6%2595%25B0%25E7%25AC%2594%25E8%25AE%25B013/11d02d66c2d85aaf67e7d625b04f48f.jpg" alt="11d02d66c2d85aaf67e7d625b04f48f" style="zoom:15%;" />

性质：

- 孩子链性质：CPI-tree中的每个2阶孩子链（直接/间接）表示一个2阶co-location表实例
- 全链性质：CPI-tree中的每个k阶全链（或间接全链）表示一个k阶co-location表实例。显然，形成全链的空间实例对应空间邻近关系图中的一个团

#### 3.2生成表实例

参考下图

<img src="./img/%E6%95%B0%E6%8D%AE%E6%8C%96%E6%8E%98%E8%AF%BB%E6%95%B0%E7%AC%94%E8%AE%B013/image-20231124160439276.png" alt="image-20231124160439276" style="zoom: 67%;" />