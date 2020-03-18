# 文本关键词生成

## TF-IDF算法：

​	这是一个广泛使用的办法，不止于文本关键字生成，主要用于统计较为文章中词语的重要程度。

​	TF指的是Term Frequency，即词频。统计

![](https://github.com/Xavxbs/nlp_practices/blob/master/image/TF.png) 

​	IDF指的是Inverse Document Frequency，即逆文本频率。计算公式如下：

![](https://github.com/Xavxbs/nlp_practices/blob/master/image/IDF.png) 

​	其中分母加1是为了防止除零错误。IDF表示出了一个词语在各个文档中的稀有程度。换言之，像“的”，“了”，”我“等这样的词语，由于在日常文本中比较常见，所以它们出现的频率会比较高。但是这种词对于某一篇文章来说，可能并没有很重要。这个时候IDF的值就会很低。

### **计算TF-IDF**

![](https://github.com/Xavxbs/nlp_practices/blob/master/image/TF-IDF.png)

​	通过上文的讲解，我们可以了解到TF与IDF分别代表了什么意思。我们想找到对于某一篇文章来说比较重要的词语，但是又不希望这个词语在各个文章中出现的频率很高（如果那样的话就表示这个词语其实对这个文章来说也不是很特别）。

​	在寻找这个很重要的词语的时候，我们通过将TF与IDF结合起来，就可以得到TF-IDF，一个可以衡量一个词语对于一个文章的重要程度。

​	TF-IDF的优点是简单快速，但是缺点在于以词频来衡了一个词的重要性可能不是很全面。比如一篇文章中的主题词并没有被反复提起，虽然人们都知道这个文章都在围绕这个关键词。还有就是对于文章中各个位置的词语，TF-IDF算法都公平对待。但是我们知道关键词一般都出现于文章的开头或者段落的开头。那我们就可以对于不同位置的词语给予不同的权重。



## TextRank算法

​	其实TextRank算法应该和RageRank算法较为相似。

​	PageRank算法的核心思想在于：

​	1.如果一个网页被很多其他网页链接到，那就说明这个网页比较重要，它的PageRank值会相对较高。

​	2.如果一个PageRank值很高的网页链接到另一个其他网页，那一个网页的PageRank值会相对提高。

​	PageRank本来是用来解决网页排名的问题，网页之间的链接关系即为图的边，迭代计算公式如下：
![](https://github.com/Xavxbs/nlp_practices/blob/master/image/PageRank.png)

​	其中，PR(Vi)表示结点Vi的rank值，In(Vi)表示结点Vi的前驱结点集合，Out(Vj)表示结点Vj的后继结点集合，d为damping factor用于做平滑。

​	TextRank 一般模型可以表示为一个有向有权图 G =(V, E), 由点集合 V和边集合 E 组成， E 是V ×V的子集。图中任两点 Vi , Vj 之间边的权重为 wji ,。对于一个给定的点 Vi, In(Vi) 为 指 向 该 点 的 点 集 合 , Out(Vi) 为点 Vi 指向的点集合。点 Vi 的得分定义如下:
![](https://github.com/Xavxbs/nlp_practices/blob/master/image/TextRank.png)

​	具体的这里还是要说一下，wji是怎么计算出来的呢？我查找了网上一些文章，都没有说明，所以还是要靠自己。我查找了jieba库中TextRank类的源代码，大概意思就是在滑动有限的大小为K窗口中，不断计算各个词（结点）之间共现（co-occurrence）的次数，这个wji就是共现的次数了。

