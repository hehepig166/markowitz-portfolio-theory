# 投资组合优化



## 参考资料

* （推荐）投资组合理论——马科维兹投资组合理论(两个风险资产的组合) https://www.bilibili.com/video/BV1vL4y1c7iH/
* （推荐）最优风险资产组合-Python https://www.jianshu.com/p/0363bc4fdad4
* Python 投资组合优化 https://www.bilibili.com/video/BV1Np4y1A7UJ
* 用python做金融数据分析 - 投资组合 https://www.bilibili.com/video/BV1Pa4y1Y7pm
* https://github.com/quantopian/research_public/blob/master/research/Markowitz-blog.ipynb
* https://youtu.be/OYrDkK5q5Lw?si=WyLikuAVqsuNGrcE
* https://zhuanlan.zhihu.com/p/671649569





## 马科维茨投资组合理论

解决问题：资产选择问题

期望收益相同的情况下选择风险最小的组合

风险相同的情况下选择期望收益最大的组合

指标（根据历史数据和当前掌握的全部信息所做出的判断）：

* 预期收益 -> 预期收益率的期望值
* 风险 -> 预期收益率的方差

### 单个证券

#### 期望收益

$$
E(r) = \sum_{i=1}^n P_i r_i
$$



#### 风险

投资收益率偏离期望值的平均程度
$$
\sigma^2 = \sum_{i=1}^n P_i [r_i - E(r)]^2
$$


### 投资组合

Q：选择若干种证券以及对应的数量，让投资者在一定收益水平下，承担的风险最小，或者在一定风险水平下收益最高。

期望收益、标准差、最小方差投资比例

#### 投资组合期望收益率

* $r$ : 投资组合收益率
* $\omega_i$ : 各个资产所占比例 ($\sum_i \omega_i = 1$)

$$
r_Q = \sum_{i=1}^n \omega_i r_i \\
\mu_Q = E(r_Q) = E(\sum_{i=1}^n \omega_i r_i) = \sum_{i=1}^n \omega_i E(r_i)
$$

#### 投资组合风险



>$$
>D(c) = 0 \\
>D(cX) = c^2 D(X)
>$$
>
>方差、协方差、相关系数
>$$
>D(X+Y) = D(X) + D(Y) + 2 cov(X, Y) \\
>cov(X, Y) = E[(X-E(X)) (Y-E(Y))] \\
>\rho_{XY} = \frac{cov(X, Y)}{\sqrt{DX} \sqrt{DY}}
>$$

$$
\begin{aligned}
\sigma_Q^2 &= D(E(r_Q)) = D(\sum_{i=1}^n E(\omega_i r_i)) \\
&= \sum_{i=1}^n \sum_{j=1}^n \omega_i \omega_j \rho_{ij} \sigma_i \sigma_j \\
&= \sum_i \omega_i^2 \sigma_i^2 + \sum_i \sum_j \omega_i \omega_j cov(r_i, r_j)
\end{aligned}
$$

#### 可行集

投资者面临的所有可能的投资组合的集合

求法：遍历所有可能权重，模拟出不同相关系数情况下各种组合的标准差和预期收益率，放在横坐标是标准差，纵坐标是期望收益率的坐标中。

#### 有效组合边界 Efficient frontier

在可行集中，所有投资者面临的既定风险水平下，最大期望收益，或既定收益水平下，最小风险水平的点的集合

求法：求出可行集后，求出全局最小方差以上的最小方差集

#### 基金分离定理

有效边界上，任意其他的点，所代表的投资组合，可以由其它点组合生成

#### 总结

* 只要掌握每组股票的风险、期望收益，以及任意两项资产间的相关系数，就能在股市上不断构造新组合
* AB组合得到一个较优点，可以用该最优点再与 C 组合得到更优点
* 不能无止境地组合，组合存在着一个边界
* 有效边界上的点都是“最优的”，高风险高收益，低风险低收益

* 投资组合没有创造新价值，只能避免承受额外的风险



## 托宾的理论

引入无风险借贷，马科维茨的有效集蜕变成一条射线

一条经过无风险资产并且与马科维茨有效集相切与一点的射线

### 资本市场线 Capital Market Line



## 项目提纲

* portfolio optimization: Markowitz Portfolio optimization in Python
* 流程
  * 获取数据
  * 计算有效边界
    * Markowitz optimization
    * Mean-variance portfolio (MVP) ?
    * Global minimum variance portfolio (GMVP)
    * Maximum Sharpe ratio portfolio (MSRP)
  * 引入无风险资产得出资本市场线
  * 得到策略结果
  * 回测
* 指标
  * 期望收益
  * 标准差
  * 夏普率
* 用到的库
  * yfinance, pandas （获取、整理数据）
  * scipy（凸优化）
  * zipline （回测）（用不了，先不弄了）
  * numpy, matplot...

## PPT

* findings
  * 资本市场线求解，初始值的选择
  * 随机很难得到最优解
