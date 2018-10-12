### SVM & HS300

1. 利用沪深300的日行情数据：开高低收、交易量，构建五个特征，以前3天的特征数据，利用基于高斯核的支持向量机分类器，预测后3天的市场涨跌方向；

2. 以10年的数据为训练集，采用网格搜索和交叉验证优化参数，其中$K-Fold$的$K$设为10，下一年的数据为测试集，依次往后滚动每隔1年构建一个新的分类器；

3. 根据预测进行多空交易，收益率为预测期间第三天的收盘价减去第一天的开盘价，并扣除一定的滑点比例

   单方向的滑点为0.0002

   如果预测正确：

   $profit = |Close_3 - Open_1|- slippage$

   如果预测失误：

   $loss =- |Close_3 - Open_1| - slippage$

   2015年1月至2018年10月的总回报考虑滑点的情况下是2.97，最大回撤44%，沪深300的总回报1.11，最大回撤47%。

   ![svm_hs300](E:\GitHub\SVM-and-HS300\data\svm_hs300.png)

4. 可以看到策略主要是在2015年完成收益率的积累，后续表现乏力，说明在趋势阶段预测效果较好，其他阶段则不如人意。

|      period      |  C   | gamma | train score | average train score（k=10) | test score |
| :--------------: | :--: | :---: | :---------: | :------------------------: | :--------: |
| 2014.11- 2015.11 |  8   | 0.02  |   0.6592    |           0.5650           |   0.5333   |
| 2015.11-2016.11  |  6   | 0.02  |   0.6329    |           0.5529           |   0.4750   |
| 2016.11-2017.11  |  5   | 0.06  |   0.7063    |           0.5517           |   0.5167   |
| 2017.11-2018.10  |  8   | 0.02  |   0.6383    |           0.5579           |   0.4566   |

### reference

[优矿，基于SVM的大盘预测](https://uqer.io/v3/community/share/56e6629e228e5b6ef3157588)