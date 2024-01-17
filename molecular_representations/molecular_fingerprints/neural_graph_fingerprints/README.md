# Neural Graph Fingerprints

[![PyPI version](https://img.shields.io/badge/github-code-red)](https://github.com/HIPS/neural-fingerprint) 

In most drug discovery by virtual screening, drugs need to be encoded as a fixed size vector, called a molecular fingeprint. One of the popular molecular fingerprint is extended connectivity fingerprint (ECFP).

In this paper, they replace the bottom layer of this stack - the function that computes molecular fingerprint vecotrs - with a differentiable neural network whose input is a graph representing the original molecule. This is an overview of neural graph fingerprint:

![neural_fp](https://cdn.jsdelivr.net/gh/BioGavin/Pic/imgneural_fp.png)

These neural graph fingerprints offer several advantages over fixed fingerprints:

- **Predictive performance.** Machine optimized fingerprints can provide substantially better predictive performance than fixed fingerprints.
- **Parsimony.** Differentiable fingerprints can be optimized to encode only relevant features, reducing downstream computation and regularization requirements.
- **Interpretability.** Each feature of a neural graph fingerprint can be activated by similar but distinct molecular fragments, making the feature representation more meaningful.



## Creating a differentiable fingerprint

This section describes the replacement of each discrete operation in ECFP with a differentiable analog.

![../../_images/neural_fp_algorithm.png](https://oi.readthedocs.io/en/latest/_images/neural_fp_algorithm.png)

- **Hashing.** They replace the hash operation with a single layer of a neural network. Using a smooth function allows the activations to be similar when the local molecular structure varies in unimportant ways.

- **Indexing.** We use the softmax operation as a differentiable analog of indexing. In essence, each atom is asked to classify itself as belonging to a single category. The sum of all these classification label vectors produces the final fingerprint. This operation is analogous to the pooling operation in standard convolutional neural networks.
- **Canonicalization.** An alternative to canonicalization is to apply a permutation-invariant function, such as summation. In the interests of simplicity and scalability, we chose summation.

If you want learn more, I found [a PowerPoint from the author of Neural Graph Fingerprints](https://www.cs.toronto.edu/~duvenaud/talks/neuralfps.pdf).



✏️ **From my personal perspective**

- Neural graph fingerprint is just like the hidden layer in MLP.
- From the perspective of encoder and decoder, the generation of neural graph fingerprints is the encoding process, and the prediction of properties with fingerprints is the decoding process.
- The generated fingerprints could be different for various prediction tasks. In other words, fingerprints as intermediates connecting molecular representations and hidden properties contain both information.

## References

- [Convolutional Networks on Graphs for Learning Molecular Fingerprints](https://papers.nips.cc/paper/5954-convolutional-networks-on-graphs-for-learning-molecular-fingerprints.pdf)
- [Neural graph fingerprint](https://oi.readthedocs.io/en/latest/bioinfo/mol_fp/neural_fp.html)

- [Practical Graph Neural Networks for Molecular Machine Learning](https://towardsdatascience.com/practical-graph-neural-networks-for-molecular-machine-learning-5e6dee7dc003)