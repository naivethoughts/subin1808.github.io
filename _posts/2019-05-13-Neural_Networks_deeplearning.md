---
layout: post
title: "Neural Network - Coursera, deeplearning.ai"
date: 2019-05-13
excerpt: "Neural Networks, Course #1 from deeplearning.ai"
tags: [Machine-Learning, Python, Neural Network]
comments: false
codes: true
---
Last updated : 06/02/2019

# Lectures

## Week 1 :
### Lecture 1 : What is a neural network?
Predictions(y) by any model depends on several parameters(x1,x2..xn). A well trained
neural network model assigns a weight to each of the parameter, based on the available
training data. The weights, thus assigned, are used to make new predictions.
### Lecture 2 : Supervised Learning with a neural network
Data come across in the form of structured data (tables,matrices etc.) and unstructured
data(images, sounds etc.). Machines were traditionally exceptional in handling structured data,
and humans in unstructured data.
### Lecture 3 : Why is deep learning taking off?
* Data : Large sets of labeled data due to digitization of the economy.
* Computation : Leaps in computational power, enabling deeper networks and more hidden layers.
* Algorithms  : Faster turn around times, reducing the time-lag for iterative improvements.

## Week 2 :
### Lecture 1 : Binary classification
For implementation, the \\( n_x \\) feature vectors are unrolled for \\( m \\) training examples,
stored as columns, for vector X. Correspondingly y is a column vector of size  \\( 1 \times m \\).

The shape of any vector can be found by
```Python
X.shape
```
out : (\\(n_x\\),m)
```Python
y.shape
```
out : (1,m)

### Lecture 2 : Logistic regression
We define logistic regression problem as for a given X, what is the probability of y to be 1.
\\[ \hat{y} \,=\,\sigma(w^T x + b) \\]

here,
\\( \sigma(z) \\) is the sigmoid function given by
\\[ \sigma(z)\,=\,\frac{1}{1+exp(-z)} \\]

b can be thought of as \\( \theta_0 \\), similar to ML course. Unlike ML, b is treated separately.

### Lecture 3 : Logistic regression : Cost function
To reach a global minima, the logistic regression uses a loss function for a single training example of the form,

\\[ \mathcal{L}(\hat{y},y)\,=\, -(y\,log(\hat{y})\,+\,(1-y)\,log(1-\hat{y}))\\]

with \\(0\,\le\,y,\hat{y}\,\le\,1\\). For y = 1, the loss function becomes
\\(\mathcal{L}(\hat{y},1)\,=\,log(\hat{y})\\) reducing to 0 as \\(\hat{y}\,\to\,1\\).

The cost function, to be minimized, is the average of loss function across all the training examples
given by,

\\[ J(w,b)\,=\,-\frac{1}{m}\,\sum_{i=1}^m\,\mathcal{L}(\hat{y}^i,y^i) \\]

If we define \\( \hat{y}\,=\,P(y=1|x) \\), that is \\( \hat{y} \\) is the probability that y = 1 for given features x. or
\\[ P(y=1|x)\,=\,\hat{y} \\]
\\[ P(y=0|x)]\,=\,1\,-\,\hat{y} \\]
This can be succinctly written as,
\\[ P(y|x)\,=\,\hat{y}^{y}(1-\hat{y})^{1-y} \\]
Taking a log on either side, would yield the cost function. The negative sign comes from the principle of maximum likelihood estimation and the scaling of \\(1/m\\) is multiplied for better convergence.

### Lecture 4 : Gradient Descent

In order to minimize the cost function \\( J(w,b) \\), gradient descent algorithm is used. To determine the direction of the
next update of \\( w \\),

\\[ w\,=\,w\,-\,\alpha\frac{\partial J}{\partial w} \\]

the above update is applied repeatedly till the value of \\( w \\) converges.

### Lecture 9 : Logistic Regression : Gradient descent

\\[ \mathcal{L}(a,y)\,=\, -(y\,log(a)\,+\,(1-y)\,log(1-a))\\]

Derivative with respect to a, would be

\\[ \frac{\partial \mathcal{L}}{\partial a}\,=\,\frac{-y}{a}\,+\,\frac{1-y}{1-a}\\]

Shows the change in loss function with respect to \\( \hat{y} \\) or \\( a \\). Now let us look into the derivative of z,

\\[ \frac{\partial a}{\partial z}\,=\,\frac{exp(-z)}{(1+exp(-z))^2}\\]
\\[ \frac{\partial a}{\partial z}\,=\,a\times(1-a)\\]

Therefore \\(dz\,=\,\frac{\partial \mathcal{L}}{\partial a}\frac{\partial a}{\partial z}\\),

\\[dz\,=\,a\,-\,y\\]

and the variables are updated as

\\[ w_i\,=\,w_i\,-\,\alpha\,x_i\, dz\\]
\\[ b_i\,=\,b_i\,-\,\alpha\,dz\\]

### Lecture 10, 15 : Logistic Regression : Gradient descent for m training examples

The vectorized implementation for logstic regression problem with m training examples is described below.

```Python
import numpy as np

for iter in range(1000) :
  Z = np.dot(w.T,X) + b
  A = sigmoid(Z)
  dZ = A - Y
  dW = (X*dZ.T)/m
  dB = np.sum(dZ)/m
  W = W - alpha*dW
  B = B - alpha*dB
```

### Lecture 11, 12, 13, 14 Vectorization, Broadcasting, Python/Numpy Vectors

* Avoid for loops, and whenever possible vectorize the code to take advantage of efficient parallelization of the language for CPUs and GPUs.
* Numpy has mathematical functions that can help in vectorization of the code.
* Broadcasting, works analogously to bsxfun in matlab and octave. For any addition, subtraction, multiplication and division operation of an (m,n) matrix with a second matrix, the second matrix is copied in m rows if the matrix is of the size (1,n) and n columns if the second matrix is of the size (m,1). Thus the second matrix is of the size (m,n) and the operation is performed.
* For easy readability and less bugs, assertain the size of matrix being operated on.
* Ensure the variable is a matrix not a rank 1 array.

## Week 3 :

### Lecture 1 - 10 Neural Network Basics

<figure>
	<img src="{{ site.url }}/images/Neural_Network.png">
	<figcaption> Schematic neural network representation. (Source: https://towardsdatascience.com/)</figcaption>
</figure>

The figure above represents a shallow neural network of three layers, with two hidden layers and one output layer. A mental picture to understand the working of a neural network is to imagine two coloured papers crumbled together, and neural network uncrumbles the paper ball to extract two distinct colored papers. In order to extract distinct outputs, the hidden layers implement various logical gates identifying similar characteristics of the inputs leading to the same output. The logical gates are implemented in the hidden layers via non linear activation functions, whereas linear activation functions would only scale the input parameters.

The hidden layer nodes and weights are initialized with random values close to zero, the random values are essential to ensure different nodes in each layer result in different gates. Thus, random value initialization for different weights is required for symmetry breaking ensuring different logical gates. The weights has to be initialized close to zero, since the activation functions : sigmoid and hyperbolic tangent (tanh) tend to saturate at very high and low weights making the learning extremely slow. Mathematical forms of widely used activation function are described below.

#### Sigmoid function :
\\[ \sigma(z)\,=\,\frac{1}{1\,+\,exp(-z)} \\]
\\[ \sigma^\prime(z)\,=\,\sigma(z)(1\,-\,\sigma(z)) \\]
The function yields values in the range of 0 to 1, centered at 0.5 for \\(z\,=\,0.0\\). This function has slow learning rates for low and high values of z, the learning rates improve for values close to zero. The sigmoid function is more suited for the output layer activation of binary classification problem.

#### Hyperbolic tangent function :
\\[ tanh(z)\,=\,\frac{exp(z)\,-\,exp(-z)}{exp(z)\,+\,exp(-z)}\\]
\\[ tanh^\prime(z)\,=\,(1\,-\,tanh(z)^2)\\]
The tanh function has values from -1 to 1, with a mean at 0 for \\(z\,=\,0.0\\). This function has better learning rates and hence preferred over sigmoid activation function.

#### RELU & Leaky RELU
\\[ RELU(z)\,=\,max(0,z)\\]
\\[ RELU^\prime(z)\,=\,0\,or\,1 \\]

\\[ Leaky\,RELU(z)\,=\,max(kz,z) \\]
\\[ Leaky\,RELU^\prime(z)\,=\,k\,or\,1 \\]
with \\( 0\,\lt\,k\lt1 \\)

The training of the system consists of two steps, forward propagation in which the output layer values are calculated based on weights of different nodes across different layers. For the forward propagation consider the schematic shown above,
* Input layer features : 3
* Hidden layers : 2
* Hidden layer 1, nodes : 4
* Hidden layer 2, nodes : 4
* Output layer nodes : 1
To calculate the activation value of the first node in hidden layer 1 from activation function g(z), z has to be calculated. Each of the three input features from the input layer are scaled using three corresponding weights (w) and offset using (b), and the z value thus obtained is fed into the activation function. This process is repeated for the four nodes in the hidden layer 1, thus we end up with a weight matrix of the size (4,3) and an offset matrix of size (4,1). The above mentioned process when applied to the second hidden layer yields a weight matrix of the size (4,4) and an offset matrix of the size (4,1). For the output layer, the weight matrix is of the size (1,4) and the offset matrix has the size (1,1). From the final activation function, the output value is obtained for the weights in the hidden layer.

The second step in the training of a neural network is the backward propagation. This step assumes the activation functions to be differentiable and using the chain rule backward propagation step determine the direction in which weights and offsets has to be shifted to reduce the cost function.

### Vectoized Algorithm
#### Forward propagation
\\[Z^{[1]}\,=\,W^{[1]}X\,+\,b^{[1]}\\]
\\[A^{[1]}\,=\,g(Z^{[1]})\\]
\\[Z^{[2]}\,=\,W^{[2]}A^{[1]}\,+\,b^{[2]}\\]
\\[A^{[2]}\,=\,g(Z^{[2]})\\]
\\[Z^{[3]}\,=\,W^{[3]}A^{[2]}\,+\,b^{[3]}\\]
\\[A^{[3]}\,=\,g(Z^{[3]})\\]

### Backward propagation
\\[dZ^{[3]}\,=\,A^{[3]}\,-\,y\\]
\\[dW^{[3]}\,=\,dZ^{[3]}(A^{[2]})^\prime\\]
\\[db^{[3]}\,=\,dZ^{[3]}\\]

\\[dZ^{[2]}\,=\,(W^{[2]})^\prime dz^{[2]}*g^\prime(Z^{[2]})\\]
\\[dW^{[2]}\,=\,dZ^{[2]}(A^{[1]})^\prime\\]
\\[db^{[2]}\,=\,dZ^{[2]}\\]

\\[dZ^{[1]}\,=\,(W^{[1]})^\prime dz^{[1]}*g^\prime(Z^{[1]})\\]
\\[dW^{[1]}\,=\,dZ^{[1]}(X)^\prime\\]
\\[db^{[1]}\,=\,dZ^{[1]}\\]

## Week 4 : Deep Neural networks

Deep neural networks consists of multiple layers, with multiple activation nodes, processing the input features to generate the output. In a naive sense, progressively the hidden layers extract and synthesis complex attributes from the input layer features. For example for a photo of a face, the first few layers might remove the background noise and extract edges, the next few layers extract the facial features, from the facial features thus extracted next layers might recompose and detect the face. Furthermore, deep learning ensures the number of nodes required to represent a complex logical gate are reduced to \\(O(log(n))\\) from \\(2^{n-1}\\) for a single layered neural network.

<figure>
	<img src="{{ site.url }}/images/Forward_Backward_propagation.JPG">
	<figcaption> Schematic forward and backward propagation. (Source: Course Slide)</figcaption>
</figure>

Any layer, in a deep neural network, can be thought of as a block which takes in activation from \\(A_{l-1}\\) as input and is operated upon by \\(W_l,\,b_l\\) to form \\(z_l\\) acted on by activation function \\(g_l\\) to produced the output \\(A_{l}\\) passed on to the next block. In the backward propagation step, \\(dA_{l}\\) is the input producing the output of \\(dA_{l-1}\\), and in the process it requires cached \\(z_l,\,W_l,\,b_l\\) from forward propagation. The update for the weights \\(dW_l\\) and \\(db_l\\) are calculated in this backward propagation.

From the discussions above, it is clear that the parameters controlling the efficiency of the neural networks are weights and offsets, \\(W_l\,\&\,b_l\\). However, the values of these parameters depends on hyperparameters such as :
* Learning rate, \\(\alpha\\)
* \# iterations
* \# hidden layers
* \# hidden nodes per layers (units)
* Choice of activation functions
* Momentum
* Mini batch size
* Regularization

The choice of parameters has a significant influence on the outputs, hence for each problem the sanity check has to be done to ensure better performance of the trained network.
