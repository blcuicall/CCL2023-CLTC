# 赛道二（中文语法错误检测）数据集

本页面主要内容为：

- [1. 数据集下载](#1-数据集下载)

- [2. 结果提交格式](#2-结果提交格式)

## 1. 数据集下载

### 1.1 训练集

本赛道提供两个汉语学习者数据集：

- CGED 历届数据

> 下载地址：https://github.com/blcuicall/cged_datasets
>
> 参赛者可以使用 cged2021 中的数据作为开发数据。

- 中文 Lang8 数据集

> 下载地址：https://pan.baidu.com/s/1Txmx7cdUrDRp5l3X9UvsgQ 
>
> 访问密码：eSPB

各参赛队伍所使用的汉语学习者（即汉语作为第二语言）数据，仅限本届大赛公开的CGED历届数据和大赛公开的Lang8数据，**不得使用其他汉语学习者数据**。其他语言数据（如汉语母语数据）不作限制。允许以各种策略或预训练模型生成伪训练数据。

### 1.2 测试集

测试集样例（测试集将包含一定比例正确句子）可参见历届测试集。

## 2. 结果提交格式

提交样例如下，也可参见历届测试集答案。

**注意：可以使用 [metrics/track2](https://github.com/blcuicall/CCL2022-CLTC/tree/main/metrics/track2) 中的 `pair2edits_word/char.py` 脚本将平行句对转为下方的 edits 格式。**

```
1,	32,	32,	M,	然后
1,	6,	6,	M,	从
2,	correct
3,	30,	30,	M,	里
4,	correct
5,	correct
6,	9,	9,	R
6,	27,	28,	S,	纷纷, 分开
6,	26,	27,	S,	纷纷, 分开, 纷
7,	correct
8,	26,	26,	S,	奖
8,	20,	20,	M,	了
9,	61,	62,	S,	丰富, 积累
10,	12,	13,	S,	新加
```

提交前，文件需依规范正确命名，并压缩成 `.zip` 格式文件的压缩包。

提交结果命名：

```
track2_test.zip	#压缩包名字
    └── cged.pred.txt	# 结果文件
```

