* Propose distributed language model according to the client/server architecture that is suitable for large corpora
* Use N-best list for re-ranking translation hypotheses
    * applied in machine translation task
* Additional sentence likelihood metrics:
    * **L0**: Count how many n-grams are matched in training corpus
    * **L1**: Average interpolated n-gram conditional probablity (unsmoothed MLE estimations for language model and weighted average)
    * **L3**: Sum of (matched) n-gram's non-compositionality
        * cut each matched n-gram into two shorter n-grams and compute point-wise mutual information (PMI) between them.
        * non-compositionality := minimal PMI of all cuts
* Instead of computing n-gram counts offline, use suffix array and count on-the-fly
    * avoid large files to store corpus' n-gram counts
* Distributed language model
    * split large training corpus into non-overlapping chunks
    * each server loads one chunk with its suffix array index
    * client sends sentence to all servers and requests count information and computes its likelihood
* Questions whether 'more data' or 'relevant data' matters more in language modelling
    * define corpora's relevance to a sentence using sum of L0 (coverage of n-grams in N-best list)
    * client now sends N translation hypotheses to all servers
    * compute for each returned n-gram matching information the relevance score and selects the m-most relevant servers
    * only use counts from these m-most relevant servers for likelihood computation 
    * use of weights also possible instead of selecting m servers
* Proposed approximated oracle-best translations by utilizing BLEU
* Standard language model training = split data into chunks and subsample count files to entries where words are listed in vocabulary of N-best list => merge sub-sampled files
    * 4-gram language model is 13GB large (could not fit into memory at that time)

# Evaluation: English Gigaword corpus and English side of ZH-EN LDC data

* 2.97B words split into 150x~20M word chunks
* trigram language model with modified Kneser-Ney smoothing (KN)
* 1,000-best list generated on 919 sentences from MT03 Chinese-English evaluation set
* 150 corpus information servers on 26 machines connected via ethernet LAN
    * one client sends each hypothesis to all 150 servers + uses re-ranking on returned information; takes ~600 seconds
* Use of bootstrapping (95% conf. int.) and BLEU

* corpora's relevance not indicating true 'relevance' (missmatch in experiments)
* Baseline=31.44 BLEU
    * Best distributed LM=32.64 BLEU (20 relevant chunks using **L2**)
         * Using 5 relevant chunks with **L2** results in 32.61 BLEU
    * 4-gram KN=32.22 BLEU