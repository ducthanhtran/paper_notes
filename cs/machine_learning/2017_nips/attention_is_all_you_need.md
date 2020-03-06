* Use of self-attention components and positional encodings to enable machine translation in a purely feed-forward fashion
* Use multiple heads in attention computations to alleviate the problem of softmax collapsing onto few positions with high value
* Feed-forward sublayers used to compose a unified representation of all attention heads
* Apply layer normalization and dropout after each sublayer
* Faster training than RNN-based networks: 
* Improvement in BLEU on WMT 2014 English-German and English-French data sets