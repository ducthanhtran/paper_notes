# Does Neural Machine Translation Benefit from Larger Context?
* ArXiv April 2017

**Authors**:
* Jean, Sebastien
* Lauly, Stanislas
* Firat, Orhan
* Cho, Kyunghyun

## Key points
	* RNN + attention architecture
	* take last n and next n' sentences as additional context information. Larger context model:
		* each context sentence s is mapped to attentional-context-vector c_{j,s} with its own encoder (bi-directional)
		* final decoder state is then dependent on all c_{j,s} for the step j and the original context vector s_{j} from the attention mechanism 
		* the attention scores alpha_{i,j}^s also depend on the final and regular context vector s_{j} with the current sentence.
	* not known how larger context affects MT, but it is known that a larger context allows the MT system to capture style, genre, topical patterns, discourse coherence and anaphora. But its impact is to be researched.
		* therefore in addition to BLEU the authors used pronoun prediction accuracy (macro-averages recall) for evaluation

## Experiments
	* WMT 2016 shared task on cross-lingual pronoun prediction
		* EN-FR: 2,411,410 sentence pairs for training
		* EN-DE: 2,356,313 sentence pairs for training
		* already preprocessed: tokenization, lemmatazation
		* not using POS tags that is provided for the target sides
		* model trained for maximizing translation quality, not pronoun prediction. Afterwards pronoun prediction is performed
			* input: source sentence and target sentence of which some pronouns are replaced with special token <REPLACE>
			* goal: replace these tokens by maximizing log-prob.
			* when multiple <REPLACE> tokens occur in single sentence -> try out all combinations (feasible due to small pronoun set)
	* IWSLT 2015
		* EN-DE: 194,371 sentence pairs
		* DEV: IWSLT 2012 test set: 1700 sentence pairs
		* TEST: IWSLT 2014 test set: 1305 sentence pairs

	* training criterion: max. log-likelihood
	* Optimizer: Adadelta
	* Early stopping on BLEU with validation set
	
### Results
* testing for varying training corpus sizes: 5%, 10%, 20%, 40%, 100%
* larger-context model outperforms baseline with +1.2 BLEU on 5% training size
	* also outperforming for 10% and 20% training sizes
	* for EN-FR at 100% the baseline overtakes and is 0.9 BLEU better
	* for EN-DE at 40% the baseline overtakes and is 0.4 BLEU better, at 100% also 0.5 BLEU better
* comparable results in terms of macro-average recall for cross-lingual pronoun prediction
	
## Comments
* longer runtime for multiple sentences due to own encoder/decoder and attention mechanism for each context-sentence
