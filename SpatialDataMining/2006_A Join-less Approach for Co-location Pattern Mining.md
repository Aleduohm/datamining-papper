## 2006_A Join-less Approach for Co-location Pattern Mining

### 前言

- 论文题目：A Join-less Approach for Co-location Pattern Mining
- 原文链接：[Link](https://ieeexplore.ieee.org/document/1565789)

基于全连接(join-based)的空间并置模式(Spatial Colocation Patterns)的挖掘在计算表实例时需要进行大量的连接操作，此处阅读的这篇论文提出了一种无连接的方法优化了表实例的计算过程，包括星型邻域划分和团邻域划分两种模型。

### 星型邻域划分模型（无连接的co-location挖掘算法）

无连接的co-location算法应用星型划分模型物化空间邻近关系，在识别表实例时，使用实例查找机制代替了大量的实例连接操作。

星型邻域关系的定义如下图所示，图中显示了对象A.1,A.3,B.4星型邻域关系的邻域，虚线圆的半径为自定义的邻域距离。

<div align=center>
<img src="./img/2006_A%20Join-less%20Approach%20for%20Co-location%20Pattern%20Mining/image-20231101214008886.png" alt="image-20231101214008886" style="zoom: 80%;" />
</div>

星型邻域可以分为重叠星型邻域划分和不重叠星型邻域划分（计算效率会更高），不重叠星型邻域如下图所示：

<div align=center>
<img src="./img/2006_A%20Join-less%20Approach%20for%20Co-location%20Pattern%20Mining/image-20231101224014134.png" alt="image-20231101224014134" style="zoom: 80%;" />
</div>

为提高挖掘效率，论文中使用了三步过滤机制找到所有频繁的co-location模式：属性级过滤、粗糙过滤和精细过滤。

- 属性级过滤：在产生的co-location模式中，如果co-location的任意子集不是频繁的，那么该模式被剪枝。
- 粗糙过滤：在查找的星型实例中，若实例的参与度小于阈值，该模式被剪枝。
- 精细过滤：在判断星型实例的团关系后重新计算参与度，若参与度小于阈值，该模式被剪枝。

无连接算法的基本步骤如图所示，包含以下步骤

1. 把空间数据物化为不相交的星型邻居
2. 生成候选co-location模式
3. 从星型邻居中查找候选co-location模式的实例
4. 进行粗糙过滤，产生粗糙的频繁co-location模式
5. 过滤co-location实例，检查模式的实例是否为一个团
6. 选择频繁的co-location模式

<div align=center>
<img src="./img/2006_A%20Join-less%20Approach%20for%20Co-location%20Pattern%20Mining/image-20231102154919947.png" alt="image-20231102154919947" style="zoom:80%;" />
</div>
### 团邻域划分（部分连接的co-location挖掘算法）

partial-join方法适合处理大部分空间邻近关系都在团分区内，而很少的空间邻近关系在各分区之间的数据集。给定一个空间数据集和一个邻近关系，首先需要生成不相交的团的集合。为了实现这一步，使用大小为d/√2*d/√2的矩形网格进行划分，其中d是邻近距离（在图中为圆的半径）。在一个网格中的对象就是一个团近邻。团邻域关系的定义如下图所示

<div align=center>
<img src="./img/2006_A%20Join-less%20Approach%20for%20Co-location%20Pattern%20Mining/image-20231101224203767.png" alt="image-20231101224203767" style="zoom: 80%;" />
</div>

不重叠的团邻域如下图所示

<div align=center>
<img src="./img/2006_A%20Join-less%20Approach%20for%20Co-location%20Pattern%20Mining/image-20231101224237886.png" alt="image-20231101224237886" style="zoom:80%;" />
</div>

部分连接算法的基本步骤如图所示，包含以下步骤

1. 生成团近邻和被切断的邻近关系
2. 生成候选co-location模式
3. 生成co-location模式的内部实例与外部实例
4. 继续生成下一级的内部实例与外部实例，在生成外部实例之前，使用k-1阶内部实例与k-1阶外部实例的基实例，对co-location进行一次粗糙剪枝（我的理解是level2的最后一步）

<div align=center>
<img src="./img/2006_A%20Join-less%20Approach%20for%20Co-location%20Pattern%20Mining/image-20231102192536238.png" alt="image-20231102192536238" style="zoom:80%;" />
</div>
