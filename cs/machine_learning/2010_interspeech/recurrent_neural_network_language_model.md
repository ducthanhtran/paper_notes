* Use RNN for modelling language model
* More computational heavy training than count-based models
* RNN model shall overcome disadvantage of fixed-sized context in FFNs
* Network and training details
    * sigmoid activation in hidden layers
    * init. weight for first hidden unit: random Gaussian noise with 0 mean and 0.1 variance
    * optimization algorithm: SGD with cross-entropy optimization objective
    * run test after each epoch on development data
* Map rare words (selected by threshold word count) in training data into special token 'rare' to make training more robust
* Propose *Dynamic* RNN model that also continues training during testing phase
* RNN outperforms count-based backoff language models

# Evaluation: Wall Street Journal (WSJ) data set
* Comparing to count-based Kneser-Ney smoothed 5-gram language model (KN5)
* Combined model using linear interpolation: 0.75 x RNN + 0.25 * KN5
    * Combined model achieved lower perplexity and WER decreased slightly
    * Using more training data improved results further, also for KN5 standalone - although a slight amount
* Mixture of 3x *dynamic* trained RNN + KN5 with linear interpolation as above achieved best PPL and WER: 121 PPL and 11.1 WER on WSJ development data.

Model|Training Data|PPL|WER
-----|-------------|---|-------
KN5  | 200K words  |336|16.4
RNN + KN5 | 200K words | 271 | 15.4
KN5  | 6.4M words  |221|13.5
RNN + KN5 | 6.4M words | 156 | 11.7
3x RNN dynamic|6.4M words|128|11.3
3x RNN dynamic + KN5|6.4M words|121|11.1

# Evaluation: NIST RT05 data set
* Comparison with very large count-based language models
* RNN trained on 5.4M words on selected in-domain data (meeting transcriptions and switchboard corpus data) in order to reduce training time
* *RT09* extends RT05 by additional data

Model|Training Data|WER static|WER dyn.
-----|-------------|----------|-------
4-gram (RT05) LM|1.3B words|24.5|-
4-gram (RT09) LM|1.3B+ words|24.1|-
RNN 1000 hidden units | 24.2|23.7
RNN 1000 hidden units + RT09 | 23.4|22.9
3xRNN + RT09|5.4M + 1.3B words|23.3|22.8
