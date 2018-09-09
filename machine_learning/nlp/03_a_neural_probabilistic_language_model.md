# A Neural Probabilistic Language Model
* Journal of Machine Learning Research (JMLR) Volume 3, February 2003
    * [JMLR](http://www.jmlr.org/papers/volume3/bengio03a/bengio03a.pdf)

**Authors**:
* Bengio, Yoshua
* Ducharme, Rejean
* Vincent, Pascal
* Jauvin, Christian

## Key points
* weakness of count-based language models (LMs) + smoothing
	* short history-length
	* word similarity not considered
	* curse of dimensionality
* approach: learn distributed feature vectors for each input word that lies in a continuous real-valued vector space
	* MLP, no non-linear activation function in embedding
	* one hidden layer with tanh and output layer is softmax'ed (main bottleneck)
	* may utilize direct input connection to output layer
	* SGD training
* implementation:
	* softmax runs in parallel
	* data-parallelization that runs asynchronously
	* parameter-parallelization

## Experiments
* learning rate eps=0.003 with learning rate schedule eps_t := eps_0 / (1 + rt)
	* t := #parameter updates
	* r := 10^-8 decrease factor, chosen heuristically
* early stopping on dev set - only necessary in Brown experiments
* comparing against count-based techniques
	* interpolated/smoothed trigram model by Jelinek and Mercer, 1980
	* back-off n-gram modified Kneser-Ney
	* class-based n-gram models

### Brown corpus
* 1.180M running words
	* train: 800K words
	* dev: 200K words
	* test: 180K words
	* |V| = 47K
* rare words with freq. <= 3 merged into single symbol, reducing |V| to 16K
* weight decay: 10^-4 (based on trials with dev-PPL)
* convergence: 10-20 epochs


### Associated Press (AP) News 1995/1996
* train: 14M words
* dev: 1M words
* test: 1M
* |V| = 148K -> |V| = 18K
	* keeping only most freq. words and punctuations
	* lower-casing
	* numerics -> to special symbols
	* rare words -> special symbols
	* proper nouns -> special symbol
* weight decay: 10^-5 (based on trials with dev-PPL)
* convergence: 5 epochs (> 3 weeks using 40 CPUs)


## Results
* Neural LMs are significantly better than count-based models. Perplexity difference:
	* Brown test: 24%
	* AP test: 8%
* direct input-to-output connection:
	* usage yields faster convergence: 10 instead of 20 epochs for Brown data
	* Additional input-to-output connection provide information of 'linear' part of mapping from features to log probabilities
	* without this direct connection the network might be forced to generalize more, thus lower PPL was observed
* always improving results when trigram model and neural LM are weighted together with 0.5


## Comments
* elaborate implementation-part due to low computational resources at that time
