创新点
1. dense classification
- 要解决的问题：对于一个embedding矩阵的处理 1. flattening: discriminative, not invariant
,2. global pooling: invariant, less discriminative
- 做法：拿到一个embedding矩阵(行是每一个空间位置，列是特征)，将每一个空间位置上的embedding向量去和每一个类的class weight向量(这两个向量维度相同)做scaled余弦相似度(这里的空间位置指一个区域)得到一个中间向量，再做softmax(文中说之前的操作是1x1卷积和depth-wise softmax)和交叉熵loss。最后每一个区域的loss加起来。
	- softmax之后得到的就是一个区域中所有类别的置信度向量
- 意义：最后的结果中dense classification比pooling得到更加平滑的、和目标更aligned的类激活图(文中如此说，但从图中我没太看出来)。促进网络识别目标的所有部分而不是最discriminative的地方。