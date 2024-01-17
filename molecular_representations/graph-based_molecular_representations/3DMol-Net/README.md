# 3DMol-Net

**Learn 3D Molecular Representation using Adaptive Graph Convolutional Network Based on Rotation Invariance**

- 3D structure features of molecules play an important role in biochemical function and activity prediction, which determine the properties of the drug and the binding characteristics of the target.
- 3DMol-Net was proposed to enhance the molecular representation, considering both the topology and rotation invariance (RI) of the 3D molecular structure.
- A molecular graph was constructed with soft relations related to the spatial arrangement of the 3D coordinates to learn 3D topology of arbitrary graph structure and employ an adaptive graph convolutional network to predict molecular properties and biochemical activities.



## Molecular adaptive graph representation architecture

![image-20220331201645577](https://cdn.jsdelivr.net/gh/BioGavin/Pic/imgimage-20220331201645577.png)

1. Preprocessing the datasets with the format of SMILES to generate 3D molecular conformers.

2. Constructing the 3D graph Laplacian composed of KNN Laplacian and soft Laplacian.

3. Illustrating of the RIM and Chebyshev GCN layers.

4. Obtaining graph-level 3D representation via virtual node-based attention mechanism.





### Learning 3D soft relation for graph update

- **hard relation**

If two atoms are associated, then a bond exists; otherwise, no bond exists. The above relationship between atoms is called a hard relation $\Phi_h \in \set{0,1}$.

- **soft relation**

Soft relation was designed as  $\Phi_s \in [0,1]$ to completely describe the relation between atoms.

- **mine the soft relation**

A MLP was designed to learn the edge relationship and mine the soft relation.

###### 

### Constructing 3D graph Laplacian

- **3D graph Laplacian matrix**

3D graph Laplacian matrix $Lap^{(3D)}$ Is first initialized by the $Lap^{(3D)}_{knn}$ Laplacian, and the further optimized by $Lap^{(3D)}_{rr}$ Learned through neural network. The $Lap^{(3D)}_{knn}$ is the Laplacian of an adjacency matrix obtained using the KNN algorithm. 



![image-20220331230651658](https://cdn.jsdelivr.net/gh/BioGavin/Pic/imgimage-20220331230651658.png)



### Building 3DMol-Net architecture with RI

- **RIM**

Let *F* be a mapping function that learns 3D rotation-invariant features.
$$
\bar{X} = F(RX) = F(X), X \in R^{N \times G}
$$
Where $\bar{X}$ and $X$ are the features before and after the mapping. $R$ Is an arbitrary rotation matrix



**The framework of 3DMol-Net**

![image-20220331221447678](https://cdn.jsdelivr.net/gh/BioGavin/Pic/imgimage-20220331221447678.png)

The RIM and Chebyshev GCN layer can extract 3D features of each node in a molecule. The global molecular representation can be obtained using attention.



**RI-based adaptive graph convolution algorithm for 3D molecular representation**

![image-20220331221701849](https://cdn.jsdelivr.net/gh/BioGavin/Pic/imgimage-20220331221701849.png)





## References

- [3DMol-Net: Learn 3D Molecular Representation using Adaptive Graph Convolutional Network Based on Rotation Invariance](https://ieeexplore.ieee.org/abstract/document/9454403)