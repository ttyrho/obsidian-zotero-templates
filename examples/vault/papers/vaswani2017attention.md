---
tags:
  - reference/paper/conference
aliases:
  - "Attention is all you need"
  - "vaswani2017attention"
---
# [Attention is all you need](http://papers.nips.cc/paper/by-source-2017-3058)
## Abstract
The dominant sequence transduction models are based on complex recurrent orconvolutional neural networks in an encoder and decoder configuration. The best performing such models also connect the encoder and decoder through an attentionm echanisms. We propose a novel, simple network architecture based solely onan attention mechanism, dispensing with recurrence and convolutions entirely.Experiments on two machine translation tasks show these models to be superiorin quality while being more parallelizable and requiring significantly less timeto train. Our single model with 165 million parameters, achieves 27.5 BLEU onEnglish-to-German translation, improving over the existing best ensemble result by over 1 BLEU. On English-to-French translation, we outperform the previoussingle state-of-the-art with model by 0.7 BLEU, achieving a BLEU score of 41.1.
## Annotations
+ **Figure**: <br> ![[figures/vaswani2017attention/figure-3-x182-y367.png]]<br>- On [page 3](zotero://open-pdf/library/items/UHZEYGLY?page=3&annotation=QMC7R5V3) ^QMC7R5V3
+ **Figure**: <br> ![[figures/vaswani2017attention/figure-4-x141-y553.png]]<br>- On [page 4](zotero://open-pdf/library/items/UHZEYGLY?page=4&annotation=FPY2X58Z) ^FPY2X58Z
+ **Figure**: <br> ![[figures/vaswani2017attention/figure-4-x338-y544.png]]<br>- On [page 4](zotero://open-pdf/library/items/UHZEYGLY?page=4&annotation=7UINHVAR) ^7UINHVAR
+ **Highlight**: "<mark style="background: Blue;">We trained on the standard WMT 2014 English-German dataset consisting of about 4.5 million sentence pairs. Sentences were encoded using byte-pair encoding [3], which has a shared sourcetarget vocabulary of about 37000 tokens. For English-French, we used the significantly larger WMT 2014 English-French dataset consisting of 36M sentences and split tokens into a 32000 word-piece vocabulary [31]. Sentence pairs were batched together by approximate sequence length. Each training batch contained a set of sentence pairs containing approximately 25000 source tokens and 25000 target tokens.</mark>"<br>- On [page 7](zotero://open-pdf/library/items/UHZEYGLY?page=7&annotation=2LQYL6IX) ^2LQYL6IX
+ **Highlight**: "<mark style="background: Blue;">Label Smoothing During training, we employed label smoothing of value  ls = 0.1 [30]. This hurts perplexity, as the model learns to be more unsure, but improves accuracy and BLEU score.</mark>"<br>- On [page 8](zotero://open-pdf/library/items/UHZEYGLY?page=8&annotation=N5KPHG33) ^N5KPHG33
## Related
+ [[tang2023understanding|Understanding Factual Errors in Summarization: Errors, Summarizers, Datasets, Error Detectors]]
## Metadata
+ **Topics**::  [[Representation Learning]], [[Transformer]], [[Natural Language Processing]]
+ **Authors**:: [[Vaswani, Ashish]], [[Shazeer, Noam]], [[Parmar, Niki]], [[Uszkoreit, Jakob]], [[Jones, Llion]], [[Gomez, Aidan N]], [[Kaiser, Łukasz]], [[Polosukhin, Illia]]
+ **Conference**:: [[Conference on Neural Information Processing Systems]]
+ **Year**: [[2017]]
## Resources
+ [Full text](https://arxiv.org/pdf/1706.03762.pdf)