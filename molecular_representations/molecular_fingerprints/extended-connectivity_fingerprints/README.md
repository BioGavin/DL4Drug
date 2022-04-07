# Extended-connectivity fingerprints (ECFPs)

Extended-connectiVity fingerprints (ECFPs) are a developed fingerprint methodology explicitly designed to capture molecular features relevant to molecular activity. They are well suited to tasks related to predicting and gaining insight into drug activity. Additionally, ECFPs can be used much like other fingerprints in methods, such as similarity searching, clustering, and virtual screening.



## Relation to Morgan Algorithm

ECFPs are derived using a variant of the *Morgan algorithm*, which was proposed as a method for solving the molecular isomorphism problem.



## ECFP Generation Process

The ECFP generation process has three sequential stages (for more details you can see [the notebook](extended-connectivity_fingerprints.ipynb)):

1. An *initial assignment stage* in which each atom has an integer identifier assigned to it.
2. An *iterative updating stage* in which each atom identifier is updated to reflect the identifiers of each atom’s neighbors, including identification of whether it is a structural duplicate of other features.
3. A *duplicate identifier removal stage* in which multiple occurrences of the same feature are reduced to a single representative in the final feature list. (The occurrence count may be retained if one requires a set of counts rather than a standard binary fingerprint.)

![img](https://chemicbook.com/_images/oxygen-iteration-butyramide.png)



- **About ECFP, ECFP4, and ECFP6**

The appended number is the effective diameter of the largest feature and is equal to twice the number of iterations performed; for example, if two iterations are performed, the largest possible fragment will have a width of 4 bonds, and the fingerprint name will end in “4” (e.g., “ECFP4”).



## Discussion

- **Structural Duplication**

There are cases where the identifiers are not the same but the substructures are duplicated. For example: After 2 iterations, when we take Oxygen as the center and then Nitrogen as the center, the same substructure is generated.

![img](https://chemicbook.com/_images/same-substructure-butyramide.png)

So how do we deduplicate them?

To identify such duplicates, each identifier keeps track of the set of bonds that it represents in a particular molecule. At each iteration step, the set of bonds is updated to include:

1. the union of all bonds in the central atom’s bond set from the previous iteration
2. the neighbor atom’s bond sets from the previous iteration, and
3. all attachment bonds

These bonds define the substructure within the molecule that is covered by the newly generated feature. Before the newly generated features from an iteration are appended to the fingerprint set, they are checked to see if any structural duplicates exist to either previously generated features or newly discovered features. When two features are discovered to be from equivalent bond sets, the following rules are used to remove one:

1. If the features were generated from a *different* number of iterations, the feature from the larger number of iterations is rejected.
2. If the features were generated from the *same* number of iterations, then the larger hashed identifier value (interpreted as an integer) is rejected.



- **Bit Collision**

There might still be bit collisions which can be avoided by increasing the fingerprint size further to higher values. There’s a trade-off between information stored vs sparsity in the data. While a longer fingerprint may avoid bit collisions, it also brings more sparsity in the data. Typically, a 1024 length is sufficient.

 ![img](https://docs.chemaxon.com/display/docs/images/download/attachments/1806332/cfp_generation.png) 

Few bit collisions in the fingerprint is tolerable, but too many may result in losing information in the fingerprint.



## References

- [Extended-connectivity fingerprints](https://pubs.acs.org/doi/abs/10.1021/ci100050t)

- [A beginner's guide for understanding Extended-Connectivity Fingerprints(ECFPs)](https://chemicbook.com/2021/03/25/a-beginners-guide-for-understanding-extended-connectivity-fingerprints.html)

