## 2019_Fraction-Score: A New Support Measure for Co-location Pattern Mining  

### 前言

- 论文题目：Fraction-Score: A New Support Measure for Co-location Pattern Mining
- 原文链接：[Link](https://ieeexplore.ieee.org/document/8731499)

在传统的并置模式挖掘的参与度度量方法中，参与度度量只关注特征的实例是否参与到模式中。在模式*C*中当一个特征*f*的多个实例共享另一个特征*f'*的一个实例时，每个参与实例的贡献都被记为“1”，因此，特征*f*的这多个实例的贡献被过度计算，从而导致一些模式具有较高的参与度。

如在下图中，模式{A,B}的参与度为0.5，但实际上特征A与特征B的关联性并不强。

<div align=center>
   <img src="./img/2006_A%20Join-less%20Approach%20for%20Co-location%20Pattern%20Mining/image-20231105105921382.png" alt="image-20231105105921382" style="zoom: 50%;" width=300 />
</div>

### Fraction-Score

考虑到传统参与度度量方法的不足，Chan等提出了Fraction-Score方法，该方法以分数贡献的形式反映实例间的共享关系。Fraction-Score度量方法不仅考虑了特征的实例是否参与到模式中，还考虑了实例间的共享关系。

以下图为例，计算过程如下：

<div align=center>
   <img src="./img/2006_A%20Join-less%20Approach%20for%20Co-location%20Pattern%20Mining/image-20231105112411431.png" />
</div>

1. 计算实例o对实例o'的贡献

<div align=center>
   <img src="./img/2006_A%20Join-less%20Approach%20for%20Co-location%20Pattern%20Mining/image-20231105113125610.png" alt="image-20231105113125610" style="zoom:80%;" />
</div>

   公式中Neigh(*o*'*,t,d*)表示以*o*'为中心，d为半径的圆内包含特征t的实例的数量。

   如：∆<sub>obj</sub>(*B1,A1*) = 1，∆<sub>obj</sub>(B2,A9) = 1/4

2. 计算实例*o*对特征*t*'的贡献

<div align=center>
   <img src="./img/2006_A%20Join-less%20Approach%20for%20Co-location%20Pattern%20Mining/image-20231105113851443.png" alt="image-20231105113851443" style="zoom:80%;" />
</div>

   如：∆<sub>label</sub>(*B1*,o) = min{4,1} = 1，∆<sub>label</sub>(*B2*,o) = min{1/4,1} = 1/4

3. 得到实例*o*对模式*C*中所有特征贡献最小的值（与所有特征进行计算，得到第二步中的最小值）

<div align=center>
   <img src="./img/2006_A%20Join-less%20Approach%20for%20Co-location%20Pattern%20Mining/image-20231105114948851.png" alt="image-20231105114948851" style="zoom:80%;" />
</div>

   如：∆<sub>labelSet</sub>(*B1,C*) = ∆<sub>label</sub>(*B1*,o) = 1，∆<sub>labelSet</sub>(*B2,C*) = ∆<sub>label</sub>(*B2*,o) = 1/4

4. 计算模式*C*下特征*t*的参与度（第三步得到的值求和）

<div align=center>
   <img src="./img/2006_A%20Join-less%20Approach%20for%20Co-location%20Pattern%20Mining/image-20231105115639895.png" alt="image-20231105115639895" style="zoom:80%;" />
</div>

   如：*sup(C|x)* = ∆<sub>labelSet</sub>(*B1,C*) + ∆<sub>labelSet</sub>(*B2,C*) + ... + ∆<sub>labelSet</sub>(*B5,C*) = 1 + 1/4 * 4 = 2

5. 计算模式*C*的支持度

<div align=center>
   <img src="./img/2006_A%20Join-less%20Approach%20for%20Co-location%20Pattern%20Mining/image-20231105120121420.png" alt="image-20231105120121420" style="zoom:80%;" />
</div>

   如：*sup(C)* = min{*sup(C|x)*,*sup(C*|o)}/9 = 2/9
