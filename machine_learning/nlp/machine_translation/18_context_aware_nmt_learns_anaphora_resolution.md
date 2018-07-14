# Context-Aware Neural Machine Translation Learns Anaphora Resolution
* [arXiv 2018](https://arxiv.org/abs/1805.10163)
* [ACL 2018](http://aclweb.org/anthology/P18-1117)
* Proceedings of the 56th Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers), 2018


**Authors**:
* Voita, Elena
* Serdyukov, Pavel
* Sennrich, Rico
* Titov, Ivan


## Key points
* context information is likely beneficial in translating from non-gender languages to gender-formed languages like English->Russian
    * pronoun translation takes in context-information by attention mechanism
* Transformer as basis-architecture
    * introduce encoder part like in the Transformer:
        1. Context-embedding with positional encoding
        2. Self-attention (multi-headed)
        3. Feed-Forward layer
        4. Self-Attention
        5. Feed-Forward layer
    * shared weights for encoder-part with basic-transformer encoder in steps 1,2 and 3.
        * preliminary results showed no improvement by using a seperate encoder
        * add special token at beginning of context sentences so that encoder can differentiate context from non-context sentence
    * only steps 4 and 5 are really "new"
    * only the last Transformer layer takes in the context information, first N-1 layers are the standard Transformer stuff
    * result of step 5 is then again attended by Multi-head attention mechanism and result of Transformer encoder as well. Afterwards, both are combined in a gated-sum, followed by a Feed-Forward layer which yields the final encoder result that the decoder takes as input

### Experiments ###
* OpenSubtitles2018 corpus for EN-RU
    * all sentences are extracted randomly. Overlap with at least 0.9 in order to reduce noise.
    * Train: 2M
    * Dev: 10K
    * Test: 10K
* Join-BPE with 32K merge operations
* same hyperparameters as in the original Transformer publication, i.e.
    * N=6 layers
    * h=8 attention heads
    * Embedding dimension is 512
    * Feed-Forward dimension is 2048
    * Adam and learning rate scheduler with certain formula (see paper)
    * Regulization as in the original Transformer publication (dropout=0.1, ...)

#### Results ####
* compared to basic Transformer and Transformer with concatened sentences (see [Tiedemann et al.: Neural Machine Translation with extended Context](https://github.com/ducthanhtran/paper_notes/blob/master/machine_learning/nlp/machine_translation/17_nmt_with_extended_context.md))

model|BLEU|Difference
---
Baseline | 29.46 |
---
Concatenation (2017, Tiedeman et al.) | 29.53 | +0.07
---
Context encoder (1 previous sentence) | 30.14 | +0.68
Context encoder (1 next sentence) | 29.31 | -0.15
Context encoder (1 random sentence) | 29.69 | +0.23

* attention focuses more on pronouns in context-sentences
* focusing more on context-sentences when current sentence is quite short and context-sentence is long (more information available)
    * context more useful for short sentence
    * especially at beginning of sentences
* no BLEU improvement on source length

##### Pronoun Translation #####
* also focusing on adjectives and verbs that depend on grammatical gender
* using CoreNLP open-source co-reference resolution system from Stanford
* focus on anaphoric instances of 'it', 'I', 'you' and 'yours'
    * analysis shows up to +1.2 BLEU for context-sensitive model
    * even larger increase in BLEU (up to +2.2) for pronouns having a nominal antecedent in context sentence
* 'I' and 'you'
    * low increase in BLEU
    * co-reference to 'Mr', 'Mrs', 'officer', 'Mom', 'Dad', 'honey' and 'sweetie'
    * helps disambiguate addressee and mark of familiarity
* 'it'
    * highest BLEU improvement
    * many possibilities: depending on grammatical gender of antecedent
    * analysis of these cases by training the Berkeley aligner on 10M sentences
        * +4.3 to +4.8 BLEU increase for translation into feminine or plural pronouns
        * only +0.3 BLEU increase for translations into masculine pronouns because it is more frequent

##### Anaphora Resolution #####
* hypothesis: interpret model's attention mechanism as a latent anaphora resolution
* using CoreNLP tool and human assessment in order to back up author's hypothesis
* attention mechanism agrees with human assessment in 72% of relation noun-to-pronoun

## Comments ##
* extensive analysis part by authors
* attention focuses on pronouns, thus co-referential anaphora resolution is captured
