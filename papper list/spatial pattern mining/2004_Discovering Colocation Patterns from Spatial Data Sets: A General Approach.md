### 前言
- 论文标题：Discovering Colocation Patterns from Spatial Data Sets: A General Approach
- 原文链接:[link](https://ieeexplore.ieee.org/document/1350759)
### co-location挖掘相关概念
1. 空间特征与空间实例  
   空间特征代表空间中不同种类的事物的集合，用简单的例子来说：比如我们要探索学校(一个种类的事物)与餐饮店(另一个种类的事物)在空间上是否有关系，在这个例子中，学校与餐饮店就被称为空间特征，记为F={f<sub>1</sub>,f<sub>2</sub>,...,f<sub>n</sub>}；学校用A表示，餐饮店用B表示，他俩都是一个较大的概念，学校A下有学校A.1,A.2,...A.m，餐饮店下有B.1,B.2,...B.n，A.1,B.1,A.2就被成为空间实例，实例的集合称为实例集，记为S=S<sub>1</sub>∪S<sub>2</sub>∪...S<sub>n</sub>。
2. 空间邻近关系  
   如定义一个空间邻近关系R为欧几里得距离小于等于用户给定阈值d，可以表示为R(A.3,B.1)<=>(distance(A.3,B.1)≦d)
3. 团  
   若空间实例集I中的任意两个实例都满足R近邻关系，则称I为一个团。
4. co-location模式  
   一个空间co-location模式是一组空间特征的集合c，其中c⊆F；一个co-location模式c的长度称为模式的阶。
5. 行实例与表实例  
   如果团I'包含了模式c中的所有特征，并且I'中没有任何一个子集可以包含c中的所有特征，则I'是c的一个行实例。
   例如：{A.1,B.2}是co-location{A,B}的行实例，而{A.1,B.2,B.3}不是co-location{A,B}的行实例。
   模式c的所有行实例的集合称为表实例。
6. 参与率与参与度
   <div align=center>
      <img src="https://github.com/Aleduohm/datamining-papper/assets/84367663/a0922c3c-051a-4a16-a379-cca56363219a" width="300">
   </div>
   <div align=center>
      <img src="https://github.com/Aleduohm/datamining-papper/assets/84367663/c4383c17-c4ae-4bc7-a401-0e2ec262da73" width="500" />
   </div>
### 基于全连接的co-location挖掘算法
1. 生成候选模式
2. 生成表实例
3. 剪枝
4. 产生规则
   

   
