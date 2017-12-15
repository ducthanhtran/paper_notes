# Linguistic Regularities in Continuous Space Word Representation
* HLT-NAACL June, 2013

**Authors**:
* Mikolov, Tomas
* Yih, Wen-tau
* Zweig, Geoffrey

## Key points
* real valued vectors as means of representing words via lookup-table. These act as input to neural networks.
* vectors are more favourable than using n-grams because relationships between units is not so clear in the n-gram approach.
* word representations of RNN language model examined
    * word representation = weight matrix that is multiplied with input 1-hot-vector vector
* tests
    1. syntactic test: analogy questions, base/comparative/superlative forms of adjectives, singular/plural, base/past/3rd person present tense forms of verbs
    2. semantic test: analogy questions, e.g. clothing:shirt ~ dis:bowl valid?
* Vector offset method: solving analogy questions by means of cosine distance
    * assume relationship are present as vector offsets
    * word pairs sharing a particular relation are related by same constant offset
    * question: given a:b and c:d with d unknown
        * find embedding vectors x_a, x_b and x_c (normalized)
        * y = x_b - x_a + x_c (expected representation of word y)
        * no word can exist at exact position of y, thus search for word whose embedding vector has greatest cosine similarity to y
    * in semantic test, when d is given: compute cosine similarity cos(x_b - x_a + x_c, x_d)

## Experiments
* syntactic testset:
    * 267M words from newspaper text tagged with *Penn Treebank POS tags*
    * selected 100 most frequent plural nouns, base form verbs, possesive nouns, ...
    * total test size: 8000
* semantic testset:
    * SemEval-2012 Task 2 (Measuring Relation Similarity)
    * 79 fine-grained word relations: 10 for training and 69 for testing
* RNN toolkit of Mikolov (2012) for evaluation
* vector dimensionalities: 80, 320, 640 and composite of several systems (1600)
* training on 320M words from Broadcast News data
    * 82K vocabulary
    * training criterion: maximizing log likelihood

### Results
* comparison of RNN vectors to
    * methods of Collobert and Weston (2008) [**CW**]
    * Hieracical Log-Bilinear Model vectors of Mnih and Hinton (2009) [**HLBL**]
* syntactic test:
    * RNN vectors capture more syntactic regularities than LSA ones
    * 1600 dimensions: about 39.6% accuracy
    * 640 dimensions: about 34.7% acc.
    * 320 dimensions: about 28.5% acc.
    * 80 dimensions: about 16.2% acc.
    * comparison
        * HLBL do comparatively well like RNN
        * CW performs very poorly
* semantic test:
    * RNN vectors perform the best with 1600 dimensions and 320 dimensions having little difference.
    * outperforms previous state-of-the-art on SemEval 2012 task (UTD-NB, Rink and Harabagiu, 2012)
    * CW comparable results to HLBL

## Notes
* continuous word representations can identify syntactic and semantic relationships fairly well
* increasing the dimension results in better performance, however increase is fairly small from 640 to 1600 dimensions
### Minus
* composite system with total dimension of 1600 not specified in detail
