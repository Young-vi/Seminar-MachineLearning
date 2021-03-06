本节分享的内容是线性回归，局部加权线性回归，**岭回归和lasso**.

## 正则化：
有些情况下无法按照典型回归的方法去训练模型。比如，训练样本数量少，甚至少于样本维数，这样将导致数据矩阵无法求逆；又比如样本特征中存在大量相似的特征，导致很多参数所代表的意义重复。总得来说，就是光靠训练样本进行无偏估计是不好用了。这个时候，我们就应用结构风险最小化的模型选择策略，在经验风险最小化的基础上加入正则化因子。
通过对损失函数(即优化目标)加入惩罚项，使得训练求解参数过程中会考虑到系数的大小，通过设置缩减系数(惩罚系数)，会使得影响较小的特征的系数衰减到0，只保留重要的特征。常用的缩减系数方法有lasso(L1正则化)，岭回归(L2正则化)。
> 1-范数： 即向量元素绝对值之和。  
2-范数：Euclid范数（欧几里得范数，常用计算向量长度），即向量元素绝对值的平方和再开方。

## lasso:
当正则化因子选择为模型参数的一范数的时候，那就是lasso回归了。lasso回归相比于岭回归，会比较极端。它不仅可以解决过拟合问题，而且可以在参数缩减过程中，将一些重复的没必要的参数直接缩减为零，也就是完全减掉了。这可以达到**提取有用特征**的作用。但是lasso回归的计算过程复杂，毕竟一范数不是连续可导的。
## 岭回归：
当正则化因子选择为模型参数的二范数的时候，整个回归的方法就叫做岭回归。为什么叫“岭”回归呢？这是因为按照这种方法求取参数的解析解的时候，最后的表达式是在原来的基础上在求逆矩阵内部加上一个对角矩阵，就好像一条“岭”一样。加上这条岭以后，原来不可求逆的数据矩阵就可以求逆了。
### 那么岭回归是如何解决过拟合的问题呢？
岭回归用于控制模型系数的大小来**防止过度拟合**。岭回归通过在损失函数中加入模型参数的L2正则项以平衡数据的拟合和系数的大小。 L2范数是指向量各元素的平方和然后求平方根。我们让L2范数的规则项||W||2最小，可以使得W的每个元素都很小，都接近于0，但与L1范数不同，它不会让它等于0，而是接近于0，而越小的参数说明模型越简单，越简单的模型则越不容易产生过拟合现象。
对角矩阵其实是由一个参数lamda和单位对角矩阵相乘组成。lamda越大，说明偏差就越大，原始数据对回归求取参数的作用就越小，当lamda取到一个合适的值，就能在一定意义上解决过拟合的问题：原先过拟合的特别大或者特别小的参数会被约束到正常甚至很小的值，但不会为零。
