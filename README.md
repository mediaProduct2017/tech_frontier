# tech_frontier

problem: 使用词向量的神经网络，softmax分类器系数的初始化如何做，怎么样给随机值，输入值是否需要做batch normalization，dropout怎么做，L1或者L2 normalization怎么做

## finished

problem: placeholder是二维时，不能用任意长度的list of list，必须统一成矩阵，也就是做padding，具体怎么做，有没有什么容易的办法，需要看match-lstm的实现

只要写一个函数把小于最大长度的句子都用`<blank>`对应的id补齐就可以了。

[pad_sentence_batch](https://github.com/mediaProduct2017/tf-gpu/blob/master/fasttext_similarity.py)
