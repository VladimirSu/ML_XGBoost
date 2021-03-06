# ML_XGBoost
利用XGBoost分析重庆各区县对经济发展影响因素重要性分布
# 利用XGBoost分析重庆各区影响因素重要性

## 数据集

### 时间序列：

1999-2020

### Label：

年末总人口（户籍统计）

地区生产总值

第二产业增加值

工业总产值

房屋建筑竣工面积

公路里程

### 数据集示例：

|                                |        | 1999       | 2000      | 2001        | 2002        | 2003        | 2004      | 2005      | 2006      | 2007      | 2008      | 2009      | 2010      | 2011      | 2012      | 2013      | 2014      | 2015      | 2016      | 2017        | 2018      | 2019        |    2020     |
| ------------------------------ | ------ | ---------- | --------- | ----------- | ----------- | ----------- | --------- | --------- | --------- | --------- | --------- | --------- | --------- | --------- | --------- | --------- | --------- | --------- | --------- | ----------- | --------- | ----------- | :---------: |
| 年末总人口（户籍统计）（万人） | 巴南区 | 86.7       | 86.12     | 85.97       | 85.73       | 85.63       | 85.75     | 86.19     | 86.61     | 87.19     | 87.23     | 87.5      | 88.3      | 89.06     | 89.52     | 89.81     | 90.2      | 90.62     | 91.48     | 91.88       | 93.02     | 94.15       |    94.7     |
| 年末全部就业人员数（万人）     | 巴南区 | 42.1       | 43.46     | 43.8        | 48.78       | 49.82       | 50.59     | 51.76     | 48.53     | 49.46     | 50.21     |           |           |           |           |           |           |           |           |             |           |             |             |
| 地区生产总值（万元）           | 巴南区 | 446867     | 480000    | 528140      | 600255      | 705843      | 823715    | 1008898   | 1163232   | 1425661   | 1755609   | 2433339   | 3087180   | 3950968   | 4208456   | 4659295   | 5100846   | 5683423   | 6353527   | 607092      | 7812161   | 8748221     |   8654779   |
| 第二产业增加值（万元）         | 巴南区 | 175878     | 199602    | 227380      | 275101      | 355738      | 410004    | 503426    | 625465    | 793101    | 1017418   | 1223739   | 1605832   | 2185596   | 2146608   | 1957772   | 2228021   | 2620540   | 2896162   | 239660      | 3025076   | 3471993     |   3543851   |
| 第三产业增加值（万元）         | 巴南区 | 119800     | 128028    | 145499      | 163796      | 188059      | 229046    | 309370    | 351528    | 419509    | 507212    | 965917    | 1206266   | 1425258   | 1682392   | 2289990   | 2452877   | 2612549   | 2962427   | 457930      | 4374709   | 4830612     |   4604571   |
| 工业总产值（万元）             | 巴南区 | 809319.7   | 754478    | 631971      | 806231      | 261132      | 1276953   | 1398590   | 1776711   | 2433831   | 3512517   | 3836379.4 | 4979017.8 | 5883143   | 4836305   | 5165282   | 5932723   | 6973305.9 | 8037441.9 | 6151345.6   | 6654027   | 3250349.472 | 3113234.103 |
| 房屋建筑竣工面积（万平方米）   | 巴南区 | 230.556667 | 217       | 256         | 213.66      | 225.34      | 318.37    | 423.18    | 367.57    | 378.21    | 416       | 434.4318  | 478.2117  | 554.6068  | 571.8313  | 795.93    | 593.85    | 848.8589  | 681.987   | 528.9478    | 493.06    | 576.15      |   581.06    |
| 公路里程（公里）               | 巴南区 | 1050.83726 | 1973      | 1132.411866 | 1259.942601 | 1009.693536 | 876       | 926       | 2144      | 2184      | 2491      | 2661.993  | 2657.519  | 2649.871  | 2685.214  | 2771.07   | 2835.15   | 3331.815  | 3357.001  | 3414.48     | 3498      | 3709        |    3708     |
| STD                            | 巴南区 | 7.11499413 | 7.5103901 | 7.487248151 | 8.693292399 | 9.041193271 | 10.272852 | 10.368213 | 11.336696 | 11.340746 | 11.384469 | 11.404007 | 11.42912  | 11.493846 | 11.621588 | 11.829    | 12.937212 | 14.919899 | 16.71622  | 16.84188441 | 18.803124 | 18.99803886 | 19.09696346 |
| MEAN                           | 巴南区 | 2.81913139 | 3.3062122 | 3.420010995 | 3.992303463 | 4.142935679 | 4.6641012 | 4.8202309 | 5.3315008 | 5.3936229 | 5.1896647 | 5.0797141 | 5.2979659 | 5.635514  | 6.0368334 | 6.2402419 | 7.0428807 | 8.37768   | 9.6047279 | 9.7262232   | 10.623419 | 10.79219351 | 10.87245739 |
| SUM                            | 巴南区 | 5128       | 6014      | 6221        | 7262        | 7536        | 8484      | 8768      | 9698      | 9811      | 9440      | 9240      | 9637      | 10251     | 10981     | 11351     | 12811     | 15239     | 17471     | 17692       | 19324     | 19631       |    19777    |

## 需要Python外部包

```python
import pandas as pd
import numpy as np
import xgboost as xgb
import matplotlib.pyplot as plt
```

### 输出示例

![巴南区 Xlsx](https://user-images.githubusercontent.com/24367388/175769967-1e3073cb-8c1b-4f3c-96ef-495be30ab056.png)


