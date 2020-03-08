# Using the Laplacian in Reinforcement Learning

<br>

This repository is based on the following two papers:

+ [A Laplacian Framework for Option Discovery in Reinforcement Learning (2017)](https://arxiv.org/pdf/1703.00956.pdf)
+ [The Laplacian in RL: Learning Representations with Efficient Approximations (2018)](https://arxiv.org/pdf/1810.04586.pdf)

where an attempt has been made to explore the results. Although the 2017 paper states that the proto value functions used are the eigenvectors of the Laplacian corresponding to the largest eigenvalues, the 2018 paper contradicts this by stating:

<p align=center><i>"smallest eigenvectors of the Laplacian are well-known to provide succinct representation of the geometry of a weighted graph."</i></p>

## Basic Concept
By using the Laplacian framework, we are interested in learning an <i>option</i>. This is defined as a sequence of actions to satisfy some purpose or task. An option is characterised by three components, that is, a set of starting states where the option is available, a policy used to obtain an action at every timestep during an option, and a set of terminating states. Ideally, an option should be made available at any state but the challenge is how to define the policy attached to the option and defining the set of terminal states.

The 2017 paper explains the use of eigenvectors of the Laplacian matrix to obtain some <i>eigenpurpose</i> which characterises an <i>intrinsic</i> reward signal and by defining a terminal state to be a state that has a negative Q value no matter the action, they discover <i>eigenoptions</i>. The policy for these options are computed by optimising the Value function using the <i>intrinsic</i> reward signals.

Laplace's equation for some function ![f](https://render.githubusercontent.com/render/math?math=f)
is a second-order partial differential equation that satisfies the sum of all the second-order partial derivatives of ![f](https://render.githubusercontent.com/render/math?math=f)
 is equal to zero. By solving this equation, we obtain functions that describe the topology of our domain space. If the domain space is discretised, we instead consider the Laplacian matrix and obtain vectors in place of functions. As the 2017 paper considers the gridworld, we first obtain solutions through the Laplacian matrix and not by solving Laplace's equation for a function.

 It is desirable to obtain solutions that are independent so once we have constructed the Laplacian matrix ![\ \mathbf{L}](https://render.githubusercontent.com/render/math?math=%5C%20%5Cmathbf%7BL%7D), we perform the eigenvalue decomposition i.e.
![\ \mathbf{L} = \mathbf{V\Lambda V}^{-1}](https://render.githubusercontent.com/render/math?math=%5C%20%5Cmathbf%7BL%7D%20%3D%20%5Cmathbf%7BV%5CLambda%20V%7D%5E%7B-1%7D) where the column vectors of ![\mathbf{V}](https://render.githubusercontent.com/render/math?math=%5Cmathbf%7BV%7D)
satisfy ![\mathbf{v}_i^\text{T}\mathbf{v}_j=\delta_{ij}](https://render.githubusercontent.com/render/math?math=%5Cmathbf%7Bv%7D_i%5E%5Ctext%7BT%7D%5Cmathbf%7Bv%7D_j%3D%5Cdelta_%7Bij%7D)
and ![\delta_{ij}](https://render.githubusercontent.com/render/math?math=%5Cdelta_%7Bij%7D)
is the [Kronecker delta](https://en.wikipedia.org/wiki/Kronecker_delta) function. It is these vectors that when used as <i>intrinsic</i> reward functions, yields interesting policies and are referred to as <i>eigenoptions</i>.


## Results

The implementation in this repository takes the second paper to have the more correct definition as the geometries are more stable with the general exception for the eigenvector with 0 as the corresponding eigenvalue.

In the <i>four rooms</i> environment as first shown in the 2017 paper, the first PVF is the option to either go to the closest corner of the room or go to one of the doorways i.e. a <i>bottle-neck state</i>.

<p align="center">
<img src="results/four_rooms-1.gif" width="1000" height="350" />
</p>

As the eigenvectors can be interpreted as both positive or negative, we can follow the complete opposite of a given option to get the opposite result e.g. go to the far edge of either room or go to the doorway.
<p align="center">
<img src="results/two_rooms-7.gif" width="1000" height="350" />
</p>

For the <i>hard maze</i> gridworld, the first few options describe how to get to the dead-ends.
<p align="center">
<img src="results/hard_maze-5.gif" width="1000" height="350" />
</p>

Interestingly, the <i>three rooms</i> gridworld shares the same property as the <i>four rooms</i> in the sense that the first PVF describes how to get to the corner of a room or a doorway.
<p align="center">
<img src="results/three_rooms-1.gif" width="1000" height="350" />
</p>

## Future Works

Implement the 2018 paper for a continuous state space like <i>cartpole<i/>.
