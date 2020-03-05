# rl-laplacian

<br>

This repository uses the Laplacian framework for option discovery in Reinforcement Learning as demonstrated in [this](https://arxiv.org/pdf/1703.00956.pdf) paper. Although the paper states that the proto value functions used are the eigenvectors of the Laplacian corresponding to the largest eigenvalues, another [paper](https://arxiv.org/pdf/1810.04586.pdf) contradicts this by stating:

<p align=center><i>"smallest eigenvectors of the Laplacian are well-known to provide succinct representation of the geometry of a weighted graph."</i></p>

The implementation in this repository takes the second paper to have the more correct definition as the geometries are more stable with the exception for the eigenvector with 0 as the corresponding eigenvalue.
