# Accelerated learning in layered neural networks
* Complex Systems Volume 2, 1988
    * [Wolfram](http://wpmedia.wolfram.com/uploads/sites/13/2018/02/02-6-1.pdf)

**Authors**:
* Levin, Esther
* Fleisher, Michael

## Key points
* Study an entropy-based measure as training criterion for neural networks
    * alternative names: binary cross entropy, binary/relative divergence, relative entropy
    * especially suitable for binary target output
    * see equation 2.16


## Experiments
* Contiguity problem:
    * binary input of length N
    * target output = number k of consequent 1-blocks
    * e.g. input (110011101) has target k=3
    * simpler version: differentiate between two classes k <= k_0 and k > k_0
* 1 hidden layer MLP
* constant learning rate of 0.25 and 0.125
* input layer only receives p subsequent units from input vector, not fully connected!
* set N:=10
* restricted the 2^N possible input patterns to 792
* training set of 100 randomly selected patterns
* random initialization of weights from normal distribution


## Results
* for p=2,3,...,6
    * increasing p yields worse accuracy on test set and longer training time
    * averaged results over 10 runs with different weight initializations
* learning rate of 0.125 led to less oscillations in training criterion as opposed to 0.25
* binary divergence had steeper error surface than quadratic error, tested on random samples
    * improved convergence as opposed to quadratic error training criterion
    * also outperforming on test set - small differences in accuracy though
