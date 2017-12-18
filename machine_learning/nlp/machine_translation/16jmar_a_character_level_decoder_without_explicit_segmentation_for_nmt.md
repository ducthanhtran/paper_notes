# A Character-Level Decoder without Explicit Segmentation for Neural Machine Translation
* arXiv March, 2016
* ACL August, 2016

**Authors**:
* Chung, Junyoung
* Cho, Kyunghyung
* Bengio, Yoshua

## Key points
* most machine translation systems work on word-level. Question: Can neural machine translation be done directly on character-level without an explicit segmentation?
    * previous proposed methods rely on segmentation techniques
    * use character-sequence on target side (decoder) and subword units on source-side (Byte-Pair-Encoding (BPE), see Sennrich et al., 2015)
    * introduce decoder that uses bi-scale RNN
* challenges:
    * source side: unclear how to learn mapping from spelling to meaning of sentence
    * target side: same and source side, plus generating a long and coherent character sequence is hard due to large state space.
    * in this paper: focus on target side

## Experiments
* use BPE as representation of source sentences
* evaluate on target sentences:
    * BPE
    * character sequence
* training data: from WMT 15 corpora
    * EN-CS: 12.1M sentences
    * EN-DE: 4.5M sentences
    * EN-RU: 2.3M sentences
    * EN-FI: 2M sentences
    * limit corpora
        * source side: only sentences up to 50 subword symbols
        * target side: up to 100 subword symbols or 500 characters
* development sets:
    * newstest2013 (except for EN-FI)
    * newsdev2015s (EN-FI)
* test sets
    * newstest2014 and newstest2015 (exept EN-FI)
    * newstest2015 (EN-FI)

### Models under testing
* all encoder use GRUs
    * 512 hidden units for each forward and backward direction
* decoders have 1014 hidden units per layer
* training settings
    * optimization algorithm: SGD+Adam
    * minibatch of 128 sentence pairs
    * norm of gradient clipped with threshold 1
* beam search sizes: 5 (BPE) and 15 (character-level)
    * chosen according to development set

#### Model 1: BPE to BPE
* GRU decoder

#### Model 2: BPE to character (base)
* GRU decoder

#### Model 3: BPE to Char (bi-scale)
* bi-scale RNN decoder

#### Model 4: Ensemble of neural machine translation systems

#### Model 5: SMT-based approach

### Results

## Notes
### Minus

### Plus
