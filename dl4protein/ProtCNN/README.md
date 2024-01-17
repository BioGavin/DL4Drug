# ProtCNN

[![PyPI version](https://img.shields.io/badge/github-code-red)](https://github.com/google-research/google-research/tree/master/using_dl_to_annotate_protein_universe) 

[Google Research Team bring Deep Learning to Pfam](https://xfam.wordpress.com/2021/03/24/google-research-team-bring-deep-learning-to-pfam/)

**Using Deep Learning to Annotate the Protein Universe**

The Pfam database is a large collection of protein families, each represented by **multiple sequence alignments** and **hidden Markov models (HMMs)**.

Proteins are generally composed of one or more functional regions, commonly termed **domains**.



## Main Point

**Task**

Annotate protein function in Pfam-seed and Pfam-full, respectively.

**Split**

Randomly-split, Clustered Split.

**Dataset**

- Pfam-seed ([Pfam32.0/Pfam-A.seed.gz](http://ftp.ebi.ac.uk/pub/databases/Pfam/releases/Pfam32.0/Pfam-A.seed.gz)) dataset (80%Train+10%Dev+10%Test) contains ～1.34 million curated sequences.

![image-20220426231142855](https://cdn.jsdelivr.net/gh/BioGavin/Pic/imgimage-20220426231142855.png)



- Pfam-full dataset (80%training+10%tuning+10%testing) contains ～54 million curated sequences.

![image-20220426231102936](https://cdn.jsdelivr.net/gh/BioGavin/Pic/imgimage-20220426231102936.png)

**Evaluation**

Stratify analysis by the maximum percent identity of each test sequence with sequences in the train set.



## Models

![image-20220426214039677](https://cdn.jsdelivr.net/gh/BioGavin/Pic/imgimage-20220426214039677.png)



### ProtCNN

ProtCNN processes an input sequence using two consecutive steps:

1. map the sequence to a 1,100-dimensional feature vector using multiple layers of non-linear transformations
2. apply a linear transformation to the embedding to predict family membership



Convolutional residual networks (ResNets) are used in the embedding network for training quickly and stably.



### ProtENN

Replicate deep CNN models trained with different random parameter initializations make distinct errors, leading to ProtENN, an ensemble of ProtCNN models.



### ProtREP

Compute the average learned representation for each family across its training sequences, yielding a sentinel family representation.



## Results

### Model performance on the random split of Pfam-seed

![image-20220426203240607](https://cdn.jsdelivr.net/gh/BioGavin/Pic/imgimage-20220426203240607.png)



### Model performance on the random split of Pfam-full

Pfam-full contains ～54 million sequences which were annotated by 17929 profile HMMs built from Pfam-seed.

![image-20220426211716478](https://cdn.jsdelivr.net/gh/BioGavin/Pic/imgimage-20220426211716478.png)



### Annotation using the learned embeddings

Performance when classifying using nearest neighbors in embedding space.

![image-20220427212905116](https://cdn.jsdelivr.net/gh/BioGavin/Pic/imgimage-20220427212905116.png)



### One-Shot Sequence Annotation

Contrasting methods’ performance when only a small number of sequences are made available for certain families. This shows that these embeddings can help grow families using only a few founder sequences.

![image-20220427213011649](https://cdn.jsdelivr.net/gh/BioGavin/Pic/imgimage-20220427213011649.png)



