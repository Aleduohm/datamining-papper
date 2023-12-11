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
<div align=center>
  <img src="./img/2009_An%20order-clique-based%20approach%20for%20mining%20maximal%20co-locations/image-20231207095554314.png" alt="image-20231207095554314" style="zoom:80%;" width=400/>
</div>

#### 2.4特征x的排序邻近关系集合

例如：δ<sub>A</sub>={{A.1,B.1C.1},{A.2,B.4,C.2},{A.3,B.3,C.1,C.3,D.1},{A.4,B.3}}

<div align=center>
  <img src="./img/2009_An%20order-clique-based%20approach%20for%20mining%20maximal%20co-locations/image-20231207134305996.png" alt="image-20231207134305996" style="zoom:67%;" width=300/>
</div>

#### 2.5邻近关系树

以上图为例，上图的邻近关系树如下：

<div align=center>
  <img src="./img/2009_An%20order-clique-based%20approach%20for%20mining%20maximal%20co-locations/image-20231207135437404.png" alt="image-20231207135437404" style="zoom: 80%;" />
</div>

#### 2.6表实例树

以Ins作为根节点，每个分支代表了候选模式c的一个表实例的树叫做c的表实例树

基于上图计算的到的候选极大co-location模式{A,B,C}的Ins树如下图所示
<div align=center>
  <img src="./img/2009_An%20order-clique-based%20approach%20for%20mining%20maximal%20co-locations/image-20231207140036902.png" />
</div>
生成过程可参考如下：

<div align=center>
  <img src="./img/2009_An%20order-clique-based%20approach%20for%20mining%20maximal%20co-locations/image-20231207145421856.png" alt="image-20231207145421856" width=600 />
</div>
