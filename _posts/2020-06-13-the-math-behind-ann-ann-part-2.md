---
id: 1173
title: 'The math behind ANN (ANN- Part 2)'
date: 2020-06-13T19:23:57+05:30
author: Achyuthuni Harsha
excerpt: Discussing the theory behind ANN and the math behind back-propagation.
layout: post
guid: https://www.harshaash.com/?p=1173
permalink: /the-math-behind-ann-ann-part-2/
image: /wp-content/uploads/2020/06/ANN-2.png
categories:
  - Artificial Intelligence
  - Data Sciences
tags:
  - ANN
  - Back propogation
  - derivation
  - Feedforward
  - math
  - perceptron
---
<div class="container-fluid main-container">
  <div class="fluid-row" id="header">
    <h1 class="title toc-ignore">
      The math behind ANN (ANN- Part 2)
    </h1>
    
    <h4 class="author">
      Harsha Achyuthuni
    </h4>
    
    <h4 class="date">
      13/06/2020
    </h4>
  </div>
  
  <div id="introduction" class="section level1">
    <h1>
      Introduction
    </h1>
    
    <p>
      This is second in the <a href= "https://www.harshaash.com/category/artificial-intelligence/">series of blogs</a> about neural networks. In this blog, we will discuss the backpropagation algorithm. In the <a href = "https://www.harshaash.com/ann-1/">previous blog</a>, we have seen how a single perceptron works when the data is linearly separable. In this blog, we will look at the working of a multi-layered perceptron (with theory) and understand the math behind backpropagation.
    </p>
    
    <div id="multi-layer-perceptron" class="section level3">
      <h3>
        Multi-layer perceptron
      </h3>
      
      <p>
        An MLP is composed of one input layer, one or more layers of perceptrons called hidden layers, and one final perceptron layer called the output layer. Every layer except the input layer is connected with a bias neuron and is fully connected to the next layer.
      </p>
    </div>
    
    <div id="perceptron" class="section level3">
      <h3>
        Perceptron
      </h3>
      
      <p>
        In the previous blog, we have seen a perceptron with a single TLU. A Perceptron with two inputs and three outputs is shown below. Generally, an extra bias feature is added as input. It represents a particular type of neuron called bias neuron. A bias neuron outputs one all the time. This layer of TLUs is called a perceptron.
      </p>
      
      <img src="https://www.harshaash.com/wp-content/uploads/2020/06/ANN-1.png" /> 
      
      <p>
        In the above perceptron, the inputs are x1 and x2. The outputs are y1, y2 and y3. Θ (or f) is the activation function. In the last blog, the step function is taken as the activation function. There are other activation functions such as:<br /> <strong>Sigmoid function</strong>: It is S-shaped, continuous and differentiable where the output ranges from 0 to 1.<br /> <span class="math display">\[f\left(z\right)=\frac{1}{1+e^{-z}}\]</span> <strong>Hyperbolic Tangent function</strong>: It is S-shaped, continuous and differentiable where the output ranges from -1 to 1. <span class="math display">\[f\left(z\right)=Tanh\left(z\right) \]</span>
      </p>
    </div>
    
    <div id="training" class="section level3">
      <h3>
        Training
      </h3>
      
      <p>
        Training a network in ANN has three stages, feedforward of input training pattern, backpropagation of the error and adjustment of weights. Let us understand it using a simple example.<br /> Consider a simple two-layered perceptron as shown:
      </p>
      
      <img src="https://www.harshaash.com/wp-content/uploads/2020/06/ANN-2.png" /> 
      
      <div id="nomenclature" class="section level4">
        <h4>
          Nomenclature:
        </h4>
        
        <table>
          <colgroup> <col width="20%"></col> <col width="28%"></col> <col width="25%"></col> <col width="25%"></col> </colgroup> <tr class="header">
            <th>
              Symbol
            </th>
            
            <th>
              Meaning
            </th>
            
            <th>
              Symbol
            </th>
            
            <th>
              Meaning
            </th>
          </tr>
          
          <tr class="odd">
            <td>
              <span class="math inline">\(X_i\)</span>
            </td>
            
            <td>
              Input neuron
            </td>
            
            <td>
              \(Y_k\)
            </td>
            
            <td>
              <span class="math inline">Output Neuron</span>
            </td>
          </tr>
          
          <tr class="even">
            <td>
              <span class="math inline">\(x_i\)</span>
            </td>
            
            <td>
              Input value
            </td>
            
            <td>
              <span class="math inline">\(y_k\)</span>
            </td>
            
            <td>
              Output value
            </td>
          </tr>
          
          <tr class="odd">
            <td>
              <span class="math inline">\(Z_j\)</span>
            </td>
            
            <td>
              Hidden neuron
            </td>
            
            <td>
              <span class="math inline">\(z_j\)</span>
            </td>
            
            <td>
              The output of a hidden neuron
            </td>
          </tr>
          
          <tr class="even">
            <td>
              <span class="math inline">\(\delta_k\)</span>
            </td>
            
            <td>
              The portion of error correction for weight <span class="math inline">\(w_{jk}\)</span>
            </td>
            
            <td>
              <span class="math inline">\(\delta_j\)</span>
            </td>
            
            <td>
              The portion of error correction for weight <span class="math inline">\(v_{ij}\)</span>
            </td>
          </tr>
          
          <tr class="odd">
            <td>
              <span class="math inline">\(w_{jk}\)</span>
            </td>
            
            <td>
              Weight of j to k
            </td>
            
            <td>
              <span class="math inline">\(v_{ij}\)</span>
            </td>
            
            <td>
              weight of i to j
            </td>
          </tr>
          
          <tr class="even">
            <td>
              <span class="math inline">\(\alpha\)</span>
            </td>
            
            <td>
              Learning rate
            </td>
            
            <td>
              <span class="math inline">\(t_j\)</span>
            </td>
            
            <td>
              Actual output
            </td>
          </tr>
          
          <tr class="odd">
            <td>
              f
            </td>
            
            <td>
              Activation function
            </td>
            
            <td>
              –
            </td>
            
            <td>
              –
            </td>
          </tr>
        </table>
        
        <ul>
          <li>
            <p>
              During feedforward, each input unit <span class="math inline">\(X_i\)</span> receives input and broadcasts the signal to each of the hidden units <span class="math inline">\(Z_1\ldots Z_j\)</span>. Each hidden unit then computes its activation and sends its signal (<span class="math inline">\(z_j\)</span>) to each output unit. Each output unit <span class="math inline">\(Y_k\)</span> computes its activation (<span class="math inline">\(y_k\)</span>) to form the response to the input pattern.
            </p>
          </li>
          
          <li>
            <p>
              During training, each output unit <span class="math inline">\(Y_k\)</span> compares its predicted output <span class="math inline">\(y_k\)</span> with its actual output <span class="math inline">\(t_k\)</span> to determine the error associated with that unit. Based on this error, <span class="math inline">\(\delta_k\)</span> is computed. This <span class="math inline">\(\delta_k\)</span> is used to distribute the error at the output unit back to all input units in the previous layers. Similarly, <span class="math inline">\(\delta_j\)</span> is computed for all hidden layers <span class="math inline">\(Z_j\)</span> which is propagated to the input layer.
            </p>
          </li>
          
          <li>
            <p>
              The <span class="math inline">\(\delta_k\)</span> and <span class="math inline">\(\delta_j\)</span> are used to update the weights <span class="math inline">\(w_{jk}\)</span> and <span class="math inline">\(v_{ij}\)</span> respectively. The weight adjustment is based on gradient descent and is dependent on error gradient (<span class="math inline">\(\delta\)</span>), learning rate (<span class="math inline">\(\alpha\)</span>) and input to the neuron.
            </p>
          </li>
        </ul>
        
        <p>
          Mathematically this means the following:
        </p>
        
        <div id="feedforward-loop" class="section level5">
          <h5>
            Feedforward loop:
          </h5>
          
          <ul>
            <li>
              Each input unit (<span class="math inline">\(X_i\)</span>) receives the input <span class="math inline">\(x_i\)</span> and broadcasts this signal to all units to the hidden layers <span class="math inline">\(Z_j\)</span>.
            </li>
          </ul>
          
          <p>
            Hidden layer
          </p>
          
          <ul>
            <li>
              <p>
                Each hidden unit (<span class="math inline">\(Z_j\)</span>) sums its weighted input signals <span class="math inline">\(z\_in_j=v_{0j}+\sum_{i} x_i\times v_{ij}\)</span>
              </p>
            </li>
            
            <li>
              <p>
                The activation function is applied to this weighted sum to get the output. <span class="math inline">\(z_j=f\left(z\_in_j\right)\)</span> (where f is the activation function).
              </p>
            </li>
            
            <li>
              <p>
                Each hidden layer send this signal (<span class="math inline">\(z_j\)</span>) to the output layers.
              </p>
            </li>
          </ul>
          
          <p>
            Output layer
          </p>
          
          <ul>
            <li>
              <p>
                Each output unit (<span class="math inline">\(Y_k\)</span>) sums its weighted input signals <span class="math inline">\(y\_in_k=w_{0k}+\sum_{j}z_j\times w_{jk}\)</span>
              </p>
            </li>
            
            <li>
              <p>
                The activation function is applied to this weighted sum to get the output. <span class="math inline">\(y_k=f\left(y\_in_k\right)\)</span> (where f is the activation function).
              </p>
            </li>
          </ul>
        </div>
        
        <div id="backpropagation-of-error" class="section level5">
          <h5>
            Backpropagation of error
          </h5>
          
          <p>
            Output layer
          </p>
          
          <ul>
            <li>
              The error information term (<span class="math inline">\(\delta_k\)</span>) is computed at every output unit (<span class="math inline">\(Y_k\)</span>). <span class="math display">\[ \delta_k=\left(t_k-y_k\right)f’ y\_in_k \]</span>
            </li>
            <li>
              This error is propagated back to the hidden layer. (later weights will be updated using this <span class="math inline">\(\delta\)</span>)
            </li>
          </ul>
          
          <p>
            Hidden layer
          </p>
          
          <ul>
            <li>
              Each hidden unit (<span class="math inline">\(Z_j\)</span>) sums its weighted error from the output layer <span class="math display">\[\delta\_in_j=\sum_{k}\delta_k\times w_{jk}\]</span>
            </li>
            <li>
              The derivative of the activation function is multiplied to this weighted sum to get the weighted error information term at the hidden layer. <span class="math display">\[ \delta_j=\delta\_in_j \times f^\prime\left(z\_in_j\right) \]</span> (where f is the activation function).<br />
            </li>
            <li>
              This error is propagated back to the initial layer.
            </li>
          </ul>
        </div>
        
        <div id="update-weights-and-biases" class="section level5">
          <h5>
            Update weights and biases
          </h5>
          
          <ul>
            <li>
              The weights are updated based on the error information terms <span class="math display">\[ w_{jk}\left(new\right)=w_{jk}\left(old\right)+\Delta w_{jk}\]</span> where <span class="math inline">\(\Delta w_{jk}=\alpha\times\delta_k\times z_j\)</span><br /> <span class="math display">\[v_{ij}\left(new\right)=v_{ij}\left(old\right)+\Delta v_{ij}\]</span> where <span class="math inline">\(\Delta v_{ij}=\alpha\times\delta_j\times x_i\)</span>
            </li>
          </ul>
          
          <p>
            Steps 1 to 12 are done for each training epoch until a stopping criterion is met.
          </p>
          
          <hr />
        </div>
      </div>
    </div>
    
    <div id="derivation-of-learning-rules" class="section level2">
      <h2>
        Derivation of learning rules
      </h2>
      
      <p>
        In every loop while training, we are changing the weights (<span class="math inline">\(v_{ij}\)</span> and <span class="math inline">\(w_{jk}\)</span>) to find the optimal solution. What we want to do is to find the effect of changing the weights on the error, and minimise the error using gradient descent.<br /> The error gradient that has to be minimised is given by: <span class="math display">\[E=\frac{1}{2}\sum_{k}\left(t_k-y_k\right)^2 \]</span> The effect of changing an outer layer weight (<span class="math inline">\(w_{jk}\)</span>) on the error is given by: <span class="math display">\[\frac{\partial E}{\partial w_{jk}}=\frac{\partial}{\partial w_{jk}}\frac{1}{2}\sum_{k}\left(t_k-y_k\right)^2 \]</span> <span class="math display">\[ =\left(y_k-t_k\right)\frac{\partial}{\partial w_{jk}}f\left(y\_in_k\right) \]</span> <span class="math display">\[ =\left(y_k-t_k\right)\times z_j\times f'\left(y\_in_k\right) \]</span> Therefore <span class="math display">\[ \Delta w_{jk}=\alpha\frac{\partial E}{\partial w_{jk}}=\alpha\times\left(y_k-t_k\right)\times z_j\times f^\prime\left(y\_in_k\right)={\alpha\times\delta}_k\times z_j \]</span>
      </p>
      
      <p>
        The effect of changing the weight of a hidden layer weight (<span class="math inline">\(v_{ij}\)</span>) on the error is given by:<br /> <span class="math display">\[ \frac{\partial E}{\partial v_{ij}}=\sum_{k}{\left(y_k-t_k\right)\frac{\partial}{\partial v_{ij}}f\left(y_k\right)} \]</span> <span class="math display">\[ =\sum_{k}\left(y_k-t_k\right)f^\prime\left(y\_in_k\right)\frac{\partial}{\partial v_{ij}}f\left(y_k\right) \]</span> <span class="math display">\[ =\sum_{k}\delta_kf^\prime\left(z\_in_j\right)\left[x_i\right]\ =\delta_j\times x_i\ \]</span> Therefore <span class="math display">\[ \Delta v_{ij}=\alpha\frac{\partial E}{\partial v_{ij}}={\alpha\times\delta}_j\times x_i \]</span> This way, for any number of layers, we can find the error information terms. Using gradient descent, we can minimise the error and find optimal weights for the ANN. In the next blog, we will implement ANN on the Titanic problem and compare it with logistic regression.
      </p>
    </div>
    
    <div id="reference" class="section level2">
      <h2>
        Reference
      </h2>
      
      <p>
        Fausett, L., 1994. Fundamentals of neural networks: architectures, algorithms, and applications. Prentice-Hall, Inc..
      </p>
    </div>
  </div>
</div>