# tech_frontier

problem: placeholder是二维时，不能用任意长度的list of list，必须统一成矩阵，也就是做padding，具体怎么做，有没有什么容易的办法，需要看match-lstm的实现

只要写一个函数把小于最大长度的句子都用`<blank>`对应的id补齐就可以了。

[pad_sentence_batch](https://github.com/mediaProduct2017/tf-gpu/blob/master/fasttext_similarity.py)
