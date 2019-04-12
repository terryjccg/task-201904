
## 任务 1：实时显示期权组合希腊字母的界面程序

从`http://sx-ct.ivocap.top:50015/Api/ProfitDetail/PZY_OptionVix` （Http basic authentication，验证信息另附）可以获取一个期权组合的仓位，其净持仓为`YestodayPosition + TradeVirtualLongPos + TradeVirtualShortPos` （原谅下typo...），交易时段内会实时更新。

请用熟悉的工具写一个用来显示该组合希腊字母的界面程序。

#### 注意事项

1. 标的价格和波动率可以用静态输入，根据情况选大概合理值即可
2. r_0 = 0.03

## 任务 2：获取机器学习模型的预测值

`http://sh.ivocap.top:8501/v1/models/TestModel:predict` 部署有一个tensorflow serving服务（参考[TensorFlow Serving with Docker](https://www.tensorflow.org/tfx/serving/docker)），输入特征会得到预测值。模型是一个GRU对时间序列的预测，输入格式如下：


```python
    # Batch dim
    [
        # Time dim
        # Sample 1
        [
            # t_0
            [feature1, feature2, ...], # Feature dim
            # t_1
            [feature1, feature2, ...], # Feature dim
            ...,
            # t_n
            [feature1, feature2, ...]
        ],
        # Sample 2
        [
            [...],
            [...],
            ...
        ]
        ...
    ]

```

`features.json`中有若干带有时间戳的特征，请将其重新组装成需要的格式，并输入服务来获取预测值，`predictions_sample.json`中有部分预测结果供校验。模型时间维度的长度是`30`，结果参考`predictions_sample.json`的格式保存。

#### 注意事项

1. 要求用 C# 来完成，请自行配置环境、学习语法及寻找合适的包
2. 查阅 tf serving 的有关文档来获取其 REST api 的使用细节
