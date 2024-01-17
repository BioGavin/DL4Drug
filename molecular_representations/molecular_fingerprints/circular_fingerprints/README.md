# Circular Fingerprints

Circular fingerprints: the representation of molecular structures by atom neighborhoods.


![Definition of a circular fingerprint: Incorporating information on the arrangement of heavy atoms around each central atom](https://miro.medium.com/max/700/1*0OM7jYLEHz84jC8Csoe9Lw.png)

分子中的每个重原子都会产生这种指纹。在这个例子中，除了元素原子类型之外，还使用了力场原子类型来编码原子的杂化状态。原则上，任何类型的附加信息都可以使用。(This fingerprint is generated for each heavy atom of the molecule. In this example, force field atom types are used that encode the hybridization state of atoms in addition to the elemental atom type; in principle, any type of additional information can be employed.)

1. Each heavy atom is used as as a starting point.
2. For each heavy atom, an atom type is assigned. Atom types may vary according to the technique used. 
3. For each layer, atom types are assigned to neighboring atoms.
4. At each distance from the central atom, the number of atoms with each given atom type are recorded in order to calculate descriptor values.
5. To create fingerprints for an entire molecule, previous steps are repeated for each of in the molecule.



Applications: 

- similarity searching 
- prediction of absorption, distribution, metabolism, excretion and toxicity properties
- virtual screening
- metabolism prediction
- estimation of pK<sub>a</sub> constants









