---
license: unknown
task_categories:
- tabular-classification
- graph-ml
- text-classification
tags:
- chemistry
- biology
- medical
pretty_name: MoleculeNet HIV
size_categories:
- 10K<n<100K
configs:
- config_name: default
  data_files:
  - split: train
    path: "hiv.csv"
---

# MoleculeNet HIV

HIV dataset [[1]](#1), part of MoleculeNet [[2]](#2) benchmark. It is intended to be used through 
[scikit-fingerprints](https://github.com/scikit-fingerprints/scikit-fingerprints) library.

The task is to predict ability of molecules to inhibit HIV replication.

| **Characteristic** | **Description** |
|:------------------:|:---------------:|
|        Tasks       |        1        |
|      Task type     |  classification |
|    Total samples   |      41127      |
|  Recommended split |     scaffold    |
| Recommended metric |      AUROC      |

**Warning:** in newer RDKit vesions, 7 molecules from the original dataset are not read correctly due to disallowed
hypervalent states of some atoms (see [release notes](https://github.com/rdkit/rdkit/releases/tag/Release_2024_09_1)).
This version of the HIV dataset contains manual fixes for those molecules, made by cross-referencing original
NCI data [[1]](#1), PubChem substructure search, and visualization with ChemAxon Marvin. In OGB scaffold split, used
for benchmarking, first 2 of those problematic 7 are from the test set. Applied mapping is:
```
"O=C1O[Al]23(OC1=O)(OC(=O)C(=O)O2)OC(=O)C(=O)O3" -> "C1(=O)C(=O)O[Al-3]23(O1)(OC(=O)C(=O)O2)OC(=O)C(=O)O3"
"Cc1ccc([B-2]2(c3ccc(C)cc3)=NCCO2)cc1" -> "[B-]1(NCCO1)(C2=CC=C(C=C2)C)C3=CC=C(C=C3)C"
"Oc1ccc(C2Oc3cc(O)cc4c3C(=[O+][AlH3-3]35([O+]=C6c7c(cc(O)cc7[OH+]3)OC(c3ccc(O)cc3O)C6O)([O+]=C3c6c(cc(O)cc6[OH+]5)OC(c5ccc(O)cc5O)C3O)[OH+]4)C2O)c(O)c1" -> "C1[C@@H]([C@H](OC2=C1C(=CC(=C2C3=C(OC4=CC(=CC(=C4C3=O)O)O)C5=CC=C(C=C5)O)O)O)C6=CC=C(C=C6)O)O"
"CC1=C2[OH+][AlH3-3]34([O+]=C2C=CN1C)([O+]=C1C=CN(C)C(C)=C1[OH+]3)[O+]=C1C=CN(C)C(C)=C1[OH+]4" -> "CC1=C(C(=O)C=CN1C)[O-].CC1=C(C(=O)C=CN1C)[O-].CC1=C(C(=O)C=CN1C)[O-].[Al+3]"
"CC(c1cccs1)=[N+]1[N-]C(N)=[S+][AlH3-]12[OH+]B(c1ccccc1)[OH+]2" -> "B1(O[Al](O1)N(C(=S)N)/N=C(/C)\C2=CC=CS2)C3=CC=CC=C3"
"CC(c1ccccn1)=[N+]1[N-]C(N)=[S+][AlH3-]12[OH+]B(c1ccccc1)[OH+]2" -> "B1(O[Al](O1)N(C(=S)N)/N=C(/C)\C2=CC=CC=N2)C3=CC=CC=C3"
"[Na+].c1ccc([SH+][GeH2+]2[SH+]c3ccccc3[SH+]2)c([SH+][GeH2+]2[SH+]c3ccccc3[SH+]2)c1" -> "C1=CC=C(C(=C1)[SH2+])[SH2+].C1=CC=C(C(=C1)[SH2+])[SH2+].C1=CC=C(C(=C1)[SH2+])[SH2+].[Ge].[Ge]"
```

## References
<a id="1">[1]</a> 
AIDS Antiviral Screen Data
https://wiki.nci.nih.gov/display/NCIDTPdata/AIDS+Antiviral+Screen+Data

<a id="2">[2]</a> 
Wu, Zhenqin, et al.
"MoleculeNet: a benchmark for molecular machine learning."
Chemical Science 9.2 (2018): 513-530
https://pubs.rsc.org/en/content/articlelanding/2018/sc/c7sc02664a