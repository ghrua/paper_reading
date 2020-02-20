# CAT


## Input Method

&#x1F4D8; **Input Method for Human Translators: A Novel Approach to Integrate Machine Translation Effectively and Imperceptibly, TALLIP2018**

+ Problem
  1. Current phrase generation
  2. Next phrase prediction
+ Solution
  1. To predict the phrase `h_1^n` given the segmented pinyin `y_1^n`, this paper uses a linear model to score the convertion. Besides the general features used for input method, this paper also introduces three kinds of features that related to the translation rules, hypotheses,and n-best list.
  2. 


&#x1F4D8; **Moon IME: Neural-based Chinese Pinyin Aided Input Method with Customizable Association, ACL2018**

+ Problem
  + Previous solutions to pinyin IME is quite simple...
+ Solution:
  + train a pinyin to Chinese NMT model
  + introduce an IR system for association

## Interactive Machine Translation

&#x1F4D8; **PRIMT: A Pick-Revise Framework for Interactive Machine Translation, NAACL2016**

+ Problem
  + Traditional IMT that interacts with human in a LTR order, which is onerous and cannot modify the critical errors at the end of the sentence.
+ Solution:
  + Pick a crucial error. A classification model is used to find the phrases that will lead to a BLEU improvement greater than a threshold after revision.
  + Revise the error. Using a classification model to automatically give the correction.

&#x1F4D8; **Active learning for interactive neural machine translation of data streams, CoNLL2018**

+ Problem
  + Give an set of source sentences `V`, how to select a subset `V_s`, which will be translated with an IMT system and then used to finetune the MT model. 
+ Solution
  + This paper proposed several sampling methods: QE sampling, coverage sampling, attention distraction sampling, and the ensemble of previuos methods.


&#x1F4D8; **Correct-and-Memorize: Learning to Translate from Interactive Revisions, IJCAI2019**

+ Problem
  + Not all translation errors are equally crucial
  + Some translation errors occur repeatedly
+ Solution
  + Pick and Revise.
    + Use the baseline model to get the hypotheses `{y_1, ..., y_j, ..., y_n}`.
    + Pick a word `y_j` and replace it with `y_j^r`.
    + Use a forward NMT model to regenerate the right part of `{y_j^{\prime}, ..., y_n^{\prime}}` given `{y_1, ..., y_j^r}`
    + Use a backward NMT model to regenerate the left part `{y_1^{\prime}, ..., y_{j-1}^{\prime}}` given `{y_j^{\prime}, ..., y_n^{\prime}}`
  + This paper uses a key-value memory `(<s, c>, y^r)` to remember the revision history. It also use the sentences adjacent to the testing sentence to finetune the model.

## Other Works

<!-- &#x1F4D8; **Neural Post-Editing Based on Quality Estimation, WMT2017**
 -->

&#x1F4D8; **An Exploration of Placeholding in Neural Machine Translation, MTSummit2019**

+ Question
  + Is replacing the NER or NUM, EMAIL... to placeholder tags a really good idea?
+ Solution
  + This paper explored several placeholding techniques:
    + Replace source tokens with tag + index, e.g., EMAIL1
    + Without indexing, the bipartite matching algorithm can be used to align the tag in a source sentence with the tag in a target sentence.
    + External alignment weights, e.g., attention scores, fast-align
  + The ansewer is not clear-cut
    + Baseline model does a decent job of translating many of these types.
    + Some of the items being masked cannot be perfectly predict. For example, "It's NUMBER" -> "It's NUMBER pm", where NUMBER is a mask for 14:00 
    + Unindexed masking can do a good job of passing items through, compared to indexing system. In situations where it is better to drop the identified term than to mistranslate it, unindexed masking may be preferable.
