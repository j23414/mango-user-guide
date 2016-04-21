# Neural Networks

**Topics**
* What is a McCulloch and Pitts Neural Network?
* How do we model this artificial neural network using Gel?

## What is a McCulloch and Pitts Neural Network?

While originally designed to model real neurons in the brain, artificial neural networks have been an on-again off-again topic in machine learning. As new artificial intelligence systems are designed to drive cars, beat games, and cator to changing customer needs; artificial neural network is one of many AI methods to receive a resurgence of interest. Visualizing and simulating these neural networks may help AI researchers fine tune this complex system when answering real world questions.

The simplest neural network model was proposed by McCulloch and Pitts in 1943 and is explained as follows:

Each neuron acts as a binary threshold unit. More specifically, a neuron computes a weighted sum of its inputs from other neurons, outputing 1 or 0 depending on if that sum is above or below a particular threshold.

$$n_j(t+1)=\Theta\left(\sum_i w_{ij}n_i(t)-\mu_i\right)
\quad \text{where}\quad
\Theta(x)=\begin{cases}
	1 & \quad \text{if }x\ge 0;\\
	0 & \quad \text{otherwise}
\end{cases}$$

The terms $$n_i$$, $$n_j$$, $$t$$, and $$w_{ij}$$ represents the input neuron, output neuron, current neural net layer, and propagation weight from input to output neuron respectively.

## How do we model this artificial neural network using Gel?

The artificial neural network, like other networks, have a set of nodes and links. These nodes and links have a set of their corresponding attributes. For each node, we have a current sum variable, a temperary sum variable, and a threshold value. We may also choose to record the layer of the neuron in the overall network, although this is not required for the computation.

```
node(string id, int layer, float threshold, float sum, float temp) nt;
```

We will be using the **foreach link** statement to propagate and compute each value of the neural network. Each link will be directional, going from $$n_i$$ to $$n_j$$ and will have a propagation weight value. The value can be positive (*excitatory*) or negative (*inhibitory*).

```
link<float weight> lt;  /* the < > symbols defines a directional link */
```

We have provided a small neural network file called **neuralnet.txt** to load into Mango. Right-click and download from [here](files/neuralnet.txt)

From Mango, use File/Open to open **neuralnet.txt** in the editor window. This will also set the **neuralnet.txt** location as your current directlry. 

Create a new gel script file by typing **Ctrl+N** on Windows or Linux or **Cmd+N** on Mac. Copy the following commands into your gel script file. Press **Ctrl+S** or **Cmd+S** to save your script. 

Highlight all commands and press **Ctrl+Return** (Windows or Linux) or **Cmd+Enter** (Mac) to execute the commands and load in the neural network.

```
node(string id, int layer, float threshold, float sum, float temp) nt;
link<float weight> lt;  
graph(nt,lt) nn=import("neuralnet.txt",",");
```
