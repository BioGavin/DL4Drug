# Geometry-Based Constrained Variational Autoencoder (GEOM-CVAE)

## Introduction

在药物发现领域，寻找具有所需化学性质的候选药物分子是一项至关重要的挑战。通过神经网络的模型生成具有某些特定性质的药物分子，已经显示出加速药物发现过程的强大潜力，该过程试图以数据驱动的方式探索更广阔的化学空间。

以往关于分子生成的工作：

- 1D SMILES 不能捕捉长距离依赖，由于忽略分子结构特征，无法学习平滑的分子嵌入
- 2D 分子图更容易直观地表达分子，但对于类似的分子图，它们往往具有非常不同的 3D 结构和分子性质。

1D 和 2D 的特征编码将特征的发现限制在预先定义的分子1D 或 2D 结构中，然而空间结构是决定分子性质和理解其在物理世界中作用原理的最关键因素之一，捕捉三维空间结构特征对于分子生成至关重要。

论文基于**几何嵌入**的分子生成模型，提出一种新颖的约束变分自编码器。



## Methods

Overview of the geometry-based molecular generation by using constrained VAE.

![image-20220321202217495](https://cdn.jsdelivr.net/gh/BioGavin/Pic/imgimage-20220321202217495.png)



including four modules:

- 基于 3D 空间结构的分子可视化表征 (3-D structure-based molecular visual representation module)

将分子空间坐标转换为类似图片的 RGB 属性后使用 CNN 进行特征提取，然后进入 VAE 模型。

![img](https://pic2.zhimg.com/80/v2-2091def4f3b1e33a70ee0b816d10db5d_720w.jpg)



- 基于蛋白质表面的几何特征的图表征 (geometry-based protein graph representation module)

蛋白质的结构以 3D 网格的形式表示，并通过基于曲率的二次误差度量算法简化了网格结构至原来的1/5。每一次蛋白质结构的简化都伴随着 Chebyshev 图卷积的操作。每一次网格的简化也可以看作是图采样和图神经网络中的图池化。GGC 网络中最后两层的输出输入到 GEOM-CVAE 的解码器为限制条件。

![img](https://pic4.zhimg.com/80/v2-4aa8fc94efec249a8434fc7153af47e7_720w.jpg)



- 基于几何表示的约束变分自编码器 GEOM-CVAE (constrained VAE module)

GEOM-CVAE generates molecules with the specific properties that target the protein.

- 解析网络模块 (parser network module)

The parser network is used to obtain molecular SMILES.





## References

- [Geometry-based Molecular Generation with Deep Constrained Variational Autoencoder](https://ieeexplore.ieee.org/abstract/document/9714718)

- [IEEE TNNLS | 利用分子几何特征进行分子生成](https://zhuanlan.zhihu.com/p/478481290)