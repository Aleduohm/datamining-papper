## 2006_A Join-less Approach for Co-location Pattern Mining

### 前言

- 论文题目：A Join-less Approach for Co-location Pattern Mining
- 原文链接：[Link](https://ieeexplore.ieee.org/document/1565789)

基于全连接(join-based)的空间并置模式(Spatial Colocation Patterns)的挖掘在计算表实例时需要进行大量的连接操作，此处阅读的这篇论文提出了一种无连接的方法优化了表实例的计算过程，包括星型邻域划分和团邻域划分两种模型。

### 星型邻域划分模型（无连接的co-location挖掘算法）

无连接的co-location算法应用星型划分模型物化空间邻近关系，在识别表实例时，使用实例查找机制代替了大量的实例连接操作。

星型邻域关系的定义如下图所示，图中显示了对象A.1,A.3,B.4星型邻域关系的邻域，虚线圆的半径为自定义的邻域距离。

<img src="./img/2006_A%20Join-less%20Approach%20for%20Co-location%20Pattern%20Mining/image-20231101214008886.png" alt="image-20231101214008886" style="zoom: 80%;" />

星型邻域可以分为重叠星型邻域划分和不重叠星型邻域划分（计算效率会更高），不重叠星型邻域如下图所示：

<img src="./img/2006_A%20Join-less%20Approach%20for%20Co-location%20Pattern%20Mining/image-20231101224014134.png" alt="image-20231101224014134" style="zoom: 80%;" />

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

<img src="./img/2006_A%20Join-less%20Approach%20for%20Co-location%20Pattern%20Mining/image-20231102154919947.png" alt="image-20231102154919947" style="zoom:80%;" />

### 团邻域划分（部分连接的co-location挖掘算法）

partial-join方法适合处理大部分空间邻近关系都在团分区内，而很少的空间邻近关系在各分区之间的数据集。给定一个空间数据集和一个邻近关系，首先需要生成不相交的团的集合。为了实现这一步，使用大小为d/√2*d/√2的矩形网格进行划分，其中d是邻近距离（在图中为圆的半径）。在一个网格中的对象就是一个团近邻。团邻域关系的定义如下图所示

<img src="./img/2006_A%20Join-less%20Approach%20for%20Co-location%20Pattern%20Mining/image-20231101224203767.png" alt="image-20231101224203767" style="zoom: 80%;" />

不重叠的团邻域如下图所示

<img src="./img/2006_A%20Join-less%20Approach%20for%20Co-location%20Pattern%20Mining/image-20231101224237886.png" alt="image-20231101224237886" style="zoom:80%;" />

部分连接算法的基本步骤如图所示，包含以下步骤

1. 生成团近邻和被切断的邻近关系
2. 生成候选co-location模式
3. 生成co-location模式的内部实例与外部实例
4. 继续生成下一级的内部实例与外部实例，在生成外部实例之前，使用k-1阶内部实例与k-1阶外部实例的基实例，对co-location进行一次粗糙剪枝（我的理解是level2的最后一步）

<img src="./img/2006_A%20Join-less%20Approach%20for%20Co-location%20Pattern%20Mining/image-20231102192536238.png" alt="image-20231102192536238" style="zoom:80%;" />

## 2019_Fraction-Score: A New Support Measure for Co-location Pattern Mining  

### 前言

- 论文题目：Fraction-Score: A New Support Measure for Co-location Pattern Mining
- 原文链接：[Link](https://ieeexplore.ieee.org/document/8731499)

在传统的并置模式挖掘的参与度度量方法中，参与度度量只关注特征的实例是否参与到模式中。在模式*C*中当一个特征*f*的多个实例共享另一个特征*f'*的一个实例时，每个参与实例的贡献都被记为“1”，因此，特征*f*的这多个实例的贡献被过度计算，从而导致一些模式具有较高的参与度。

如在下图中，模式{A,B}的参与度为0.5，但实际上特征A与特征B的关联性并不强。

<img src="./img/2006_A%20Join-less%20Approach%20for%20Co-location%20Pattern%20Mining/image-20231105105921382.png" alt="image-20231105105921382" style="zoom: 50%;" />

### Fraction-Score

考虑到传统参与度度量方法的不足，Chan等提出了Fraction-Score方法，该方法以分数贡献的形式反映实例间的共享关系。Fraction-Score度量方法不仅考虑了特征的实例是否参与到模式中，还考虑了实例间的共享关系。

以下图为例，计算过程如下：

![image-20231105112411431](./img/2006_A%20Join-less%20Approach%20for%20Co-location%20Pattern%20Mining/image-20231105112411431.png)

1. 计算实例o对实例o'的贡献

   <img src="./img/2006_A%20Join-less%20Approach%20for%20Co-location%20Pattern%20Mining/image-20231105113125610.png" alt="image-20231105113125610" style="zoom:80%;" />

   公式中Neigh(*o*'*,t,d*)表示以*o*'为中心，d为半径的圆内包含特征t的实例的数量。

   如：∆<sub>obj</sub>(*B1,A1*) = 1，∆<sub>obj</sub>(B2,A9) = 1/4

2. 计算实例*o*对特征*t*'的贡献

   <img src="./img/2006_A%20Join-less%20Approach%20for%20Co-location%20Pattern%20Mining/image-20231105113851443.png" alt="image-20231105113851443" style="zoom:80%;" />

   如：∆<sub>label</sub>(*B1*,o) = min{4,1} = 1，∆<sub>label</sub>(*B2*,o) = min{1/4,1} = 1/4

3. 得到实例*o*对模式*C*中所有特征贡献最小的值（与所有特征进行计算，得到第二步中的最小值）

   <img src="./img/2006_A%20Join-less%20Approach%20for%20Co-location%20Pattern%20Mining/image-20231105114948851.png" alt="image-20231105114948851" style="zoom:80%;" />

   如：∆<sub>labelSet</sub>(*B1,C*) = ∆<sub>label</sub>(*B1*,o) = 1，∆<sub>labelSet</sub>(*B2,C*) = ∆<sub>label</sub>(*B2*,o) = 1/4

4. 计算模式*C*下特征*t*的参与度（第三步得到的值求和）

   <img src="./img/2006_A%20Join-less%20Approach%20for%20Co-location%20Pattern%20Mining/image-20231105115639895.png" alt="image-20231105115639895" style="zoom:80%;" />

   如：*sup(C|x)* = ∆<sub>labelSet</sub>(*B1,C*) + ∆<sub>labelSet</sub>(*B2,C*) + ... + ∆<sub>labelSet</sub>(*B5,C*) = 1 + 1/4 * 4 = 2

5. 计算模式*C*的支持度

   <img src="./img/2006_A%20Join-less%20Approach%20for%20Co-location%20Pattern%20Mining/image-20231105120121420.png" alt="image-20231105120121420" style="zoom:80%;" />

   如：*sup(C)* = min{*sup(C|x)*,*sup(C*|o)}/9 = 2/9
