# Modeling Past and Future for Neural Machine Translation
* [TACL 2018](http://aclweb.org/anthology/Q18-1011)
* [arXiv 2017](https://arxiv.org/abs/1711.09502)
* Transactions of the ACL, vol 6

* RNN
* Explicitly model translated past and future content (source side) in decoder
    * coverage modeling
    * functionality separation

* Use additional RNN layers for both past and future information
	* hidden state information
	* past layer: already translated source content
	* future layer: source content to be translated
* Initialization:
	* past layer: 0-vector (no past information)
	* future layer: summariziation of full source side
* Update:
	* past layer: add attention vector
	* future layer: subtract attention vector
		* modifications in GRU unit to model subtraction
* Use both past and future hidden state vector in attention mechanism and decoder state
* Loss function: additional loss for future and past layer differences (addition/subtraction)

* Data:
	* LDC ZH-EN (??? M Train)
	* WMT17 DE-EN and EN-DE (5.6M Train)
* Results:
	* Adding additional training loss yields +0.6 (past) and +0.7 (future) BLEU
	* modifications in GRU yield +0.5 BLEU
	* LDC: +2.71 BLEU-unc
		* best configuration: Future + Past + Loss + GRU-modification for Future-layer
	* WMT DE-EN: +1.9 BLEU
	* WMT EN-DE: +1 BLEU