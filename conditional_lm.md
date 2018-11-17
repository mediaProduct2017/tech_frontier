# Conditional Language Model

20181117

一般的语言模型是预测一个序列的概率，而条件语言模型是在给定一个条件的前提下，预测一个序列的概率，经常是在给定一个序列的前提下，预测另一个与之相关的序列的概率。

某些条件语言模型可以用CRF来解决，对于CRF，在预测的时候可以使用维特比算法，得到全局最优序列；但是，对于用RNN建立的条件语言模型，在预测的时候，无法得到全局最优解，通常是用greedy search, beam search或者随机搜索来得到次优解。

在评估条件语言模型时，理论上存在三种办法，一种是cross entropy，可以实现，但是很难理解，一种是task specific evaluation，比如bleu, rouge，meteor，wer，容易实现，可以理解，第三种是人工评估，实现成本巨高，但最容易理解。一般使用第二种方法。

在建立条件语言模型时，主要面临两个问题：

第一，How do we encode condition x as a fixed-size vector, c? It is problem (or at least modality) specific.（之前是这种认识，随着多任务拟合的出现，这种认识正在发生改变）

第二，How do we condition on c in the decoding model? It is less problem specific.

一种方法是计算句向量用average pooling或者cnn，cnn的好处是能够学到local context，多个相邻的local context还可能得到长距离依赖，另外，cnn有树一样的分支结构，但不需要句法分析，cnn的速度也比rnn要快。

有人说average pooling比concatenate效果要好，但也有人反着说，所以，还是要针对具体任务做评估。

问题在于，cnn一般是用于固定大小的图片的，对于句子，也要求固定大小的句子，对于短的句子可以用0补上，但是，对于长的句子，就要截断，丢失信息。用rnn理论上可以处理任意长度的句子，但是，在训练时，对于mini-batch的一批训练，RNN的长度是固定的，正因为如此，所以用到bucket，先做长度聚类。对于最新的tensorflow 不需要使用 bucketing了，直接用 dynamic rnn 就好，它会根据每个batch自动计算最好的输出，不过要更定每个example的 sequence length。当然，现在有人可以做到自动计算 sequence length了（https://www.zhihu.com/question/42057513/answer/128885542）。

常用的seq2seq，是用两个lstm，同时，输入的序列可以是正序，也可以是倒序，有时候倒序效果要更好。这个模型的问题是，encoder的output作为decoder的输入，要记住之前的太多的信息。

使用多个seq2seq模型的集成，效果有可能更好。

