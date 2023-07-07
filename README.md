# CCL 2023 汉语学习者文本纠错评测

## 最新消息

| 时间 | 消息 |
|-----| ----- |
| 7 月 7 日 | 公布获奖名单 |
| 6 月 24 日 | 更新代码和模型上交规则 |
| 6 月 16 日 | 更新评测报告须知 |
| 6 月 16 日 | 更新Baseline |
| 6 月 15 日 | 发布比赛成绩及排名 |
| 5 月 7 日 | 参赛系统提交入口开放时间变更为5月7日，关闭时间也相应推迟至6月7日 |
| 4 月 30 日 | 新增微信交流群 |

## 目录
- [1. 比赛介绍](#1-比赛介绍)
- [2. 任务内容](#2-任务内容)
- [3. 评测数据](#3-评测数据)
- [4. 评测细则](#4-评测细则)
- [5. 评价标准](#5-评价标准)
- [6. 评测赛程](#6-评测赛程)
- [7. 奖项设置](#7-奖项设置)
- [8. 论文评审](#8-论文评审)

## 1. 比赛介绍

汉语学习者文本纠错 (Chinese Learner Text Correction, CLTC) 任务旨在自动检测并修改汉语学习者文本 (Chinses Learner Text) 中的标点、拼写、语法、语义等错误，从而获得符合原意的正确句子。  

近一年随着人工智能技术的不断进步和发展，一些优秀的大规模语言模型产品逐渐进入人们的视野，如ChatGPT、文心一言、ChatGLM 等，能够自动地理解、处理和生成文本，并在自动问答、开放域对话等任务中表现出了优异的性能。这些模型的出现也为文本纠错任务的研究提供了新的机遇。  

为了推动汉语学习者文本纠错研究的发展，我们将组织新一轮评测，希望通过建立多维度、多参考答案的数据集和评价标准，进一步完善语法纠错评测，聚焦该领域中的前沿问题。我们依托第二十二届中国计算语言学大会（CCL 2023）组织本次中文语法纠错评测，既整合了已有的相关评测数据和任务，又设计了新的评测规则，希望以多赛道、多任务、统一入口的方式开展本次评测。  

**本届评测特色：** 为了探索大模型在文本纠错任务中的应用潜力，我们在本次评测的两个赛道内，分别下设了开放任务和封闭任务，共收集四个榜单。开放任务的参赛队伍可以使用包括 ChatGPT、文心一言、ChatGLM 等在内的大模型，通过调整 Prompt 等方式来实现更好的纠错效果。

- 组织者
  - 杨麟儿（北京语言大学）
  - 杨尔弘（北京语言大学）
  - 孙茂松（清华大学）
  - 刘正皓（东北大学）
  - 胡韧奋（北京师范大学）
  - 饶高琦（北京语言大学）

- 联系人
  - 常鸿翔（北京语言大学硕士生，blcuicall@163.com）
  - 刘洋（北京语言大学硕士生）
  - 徐萌（北京语言大学硕士生）
  - 周天硕（东北大学硕士生）
  - 莫凯洁（北京师范大学硕士生）
  - 王予沛（北京师范大学硕士生）

评测任务更详细内容可查看评测网站：[https://github.com/blcuicall/CCL2023-CLTC](https://github.com/blcuicall/CCL2023-CLTC)，遇到任何问题请发邮件（常鸿翔 blcuicall@163.com）或者在[Issue](https://github.com/blcuicall/CCL2023-CLTC/issues)中提问，欢迎大家参与。


## 2. 任务内容

本次评测设置下述两个赛道，每个赛道下分别设置封闭任务和开放任务。

**赛道一**：多维度汉语学习者文本纠错（Multidimensional Chinese Learner Text Correction）。同一个语法错误从不同语法点的角度可被划定为不同的性质和类型[^1]，也会因语言使用的场景不同、具体需求不同，存在多种正确的修改方案。赛道一的数据中提供针对一个句子的多个参考答案，并且从最小改动（Minimal Edit，M）和流利提升（Fluency Edit，F）两个维度对模型结果进行评测。最小改动维度要求尽可能好地维持原句的结构，尽可能少地增删、替换句中的词语，使句子符合汉语语法规则；流利提升维度则进一步要求将句子修改得更为流利和地道，符合汉语母语者的表达习惯。如表1中所示，原句在两个维度均有多个语法纠错的参考答案。

<p align='center'>表1：多参考中文语法纠错任务示例</p>
<table align='center'>
    <tr>
        <td style="text-align: center;" colspan='2'> <b>原句</b> </td>
        <td>因为我的中文没有好，我还要努力学汉语。</td>
    </tr>
    <tr>
        <td rowspan='2'><b>最小改动</b></td>
        <td>参考答案1</td>
        <td>因为我的中文<del> 没有 </del><span style="color: red;">不</span>好，我还<del> 要 </del><span style="color: red;">在</span>努力学汉语。</td>
    </tr>
    <tr>
        <td>参考答案2</td>
        <td>因为我的中文<del> 没有 </del><span style="color: red;">不</span>好，<span style="color: deepskyblue;">所以</span>我还要努力学汉语。</td>
    </tr>
    <tr>
        <td rowspan='2'><b>流利提升</b></td>
        <td>参考答案1</td>
        <td><del>因为</del>我的中文没有<span style="color: deepskyblue;">那么</span>好，<span style="color: deepskyblue;">因此</span>我还要努力学汉语。</td>
    </tr>
    <tr>
        <td>参考答案2</td>
        <td>因为我的中文<span style="color: deepskyblue;">还</span>没有<span style="color: deepskyblue;">学</span>好，<span style="color: deepskyblue;">所以</span>我还要<span style="color: deepskyblue;">更加</span>努力<span style="color: deepskyblue;">地</span>学<del> 汉语 </del><span style="color: red;">中文</span>。</td>
    </tr>
</table>

注：其中，<span style="color: red;">红字</span>表示替换字符，<span style="color: deepskyblue;">蓝字</span>表示插入字符，<del>删除线</del>表示删除字符。

<br>

**赛道二**：中文语法错误检测（Chinese Grammatical Error Diagnosis）任务目的是检测出中文文本中每一处语法错误的位置、类型。语法错误的类型分为赘余 (Redundant Words，R) 、遗漏 (Missing Words，M) 、误用(Word Selection，S)、错序 (Word Ordering Errors，W) 四类。针对M和S类错误，给出纠正结果。如表2中所示，原句的第一个错误是位置为第6到7的词“了解”，错误类型为R，即误用；第二个错误是位置为8的词“这”，错误类型为R，即赘余。

<p align='center'>表2：中文语法错误检测任务示例</p>
<table align='center'>
    <tr>
        <td style="text-align: center;">
            <b>原句</b>
        </td>
        <td>
            (sid=00038800481) 我根本不能<u>了解这</u>妇女辞职回家的现象。在这个时代，为什么放弃自己的工作，就回家当家庭主妇？
        </td>
    </tr>
    <tr>
        <td style="white-space: nowrap;">
            <b>语法错误检测</b>
        </td>
        <td>
            00038800481, 6, 7, S, 理解<br>
            00038800481, 8, 8, R
        </td>
    </tr>
</table>


## 3. 评测数据

下面分别描述每个赛道提供的评测数据集具体情况：

### **赛道一：** 多维度汉语学习者文本纠错

本次评测针对赛道一提供的数据集，包括供参赛队伍训练模型的训练集，供参赛队伍进行模型调优的开发集，以及评测参赛队伍的模型性能的封闭测试数据集。训练集来自NLPCC2018-GEC[^2]发布的采集自Lang8平台的数据。开发和测试数据来源为汉语学习者文本多维标注数据集YACLC[^3]。YACLC[^3]是一个大规模、高质量、篇章级别、多维度、多参考的中文语法纠错数据集。标注实践中采用众包策略，在搭建的可供多人同时使用的在线标注平台上分组、分任务、分阶段地进行标注和审核工作。

针对赛道一，我们提供最小改动和流利提升两个维度的两个多参考数据集YACLC-Minimal和YACLC-Fluency。其中YACLC-Minimal属于最小改动维度，YACLC-Fluency属于流利提升维度。我们从公开发布的YACLC 1.0中随机抽取了9,135句及对应的71,969句标注结果。其中的1,839句作为开发集YACLC-Minimal-Dev和YACLC-Fluency-Dev，平均参考答案的数量分别为8.67和1.81句。剩余的7,296句作为封闭测试集YACLC-Minimal-Test和YACLC-Fluency-Test，平均参考答案的数量分别为5.82和1.86句。赛道一的数据集统计信息如表3所示。

<p align='center'>表3：赛道一数据集统计</p>

|   |原句数|参考句数|平均参考句数|有修改的参考句数（比例）|原句平均字符数|参考句平均字符数|
| --- | :---: | :---: | :---: | :---: | :---: | :---: |
| YACLC-Minimal-Dev | 1,839 | 15,938 | 8.67 | 15,935(99.98%) | 25.85 | 27.22 |
| YACLC-Minimal-Test | 7,296 | 42,462 | 5.82 | 40,334(94.99%) | 21.19 | 23.25 |
| YACLC-Fluency-Dev | 1,839 | 3,332 | 1.81 | 3,332(100.00%) | 25.85 | 27.14 |
| YACLC-Fluency-Test | 5,515 | 10,237 | 1.86 | 8,604(84.05%) | 20.81 | 21.40 |

### **赛道二：** 中文语法错误检测

赛道二提供处理后的Lang8数据集和CGED数据集。CGED数据来源为HSK动态作文语料库[^4]和全球汉语中介语语料库[^5]。CGED-8共包括约1400个段落单元、3,000个错误。每个单元包含1-5个句子，每个句子都被标注了语法错误的位置、类型和修改结果。测试集样例（测试集将包含一定比例正确句子）可参见历届测试集。


## 4. 评测细则

本次评测的具体规则如下：

### 4.1 模型使用规则

- **赛道一、二开放任务**的参赛队伍可将 ChatGPT、文心一言、ChatGLM 等能够通过 API 访问的大模型用于文本纠错任务。参赛者可以撰写并调整 Prompt 直接获取大模型的语法纠错结果，或利用大模型收集语法纠错伪数据，也可以采用其他方法。

- **赛道一、二封闭任务**的参赛队伍禁止使用大模型。仅允许使用拥有开源License（如 GPL、BSD、MIT、Apache 等）且参数量小于 10B 的预训练模型。

开放任务和封闭任务的各参赛队伍所使用的方法及实验细节都应在评测报告中清晰地呈现。

### 4.2 数据集使用规则

- **赛道一封闭任务**的参赛队伍需下载组织方预处理后的Lang8数据集，仅允许采用上述数据进行训练。

- **赛道一开放任务**的参赛队伍可使用各种开源数据进行训练，允许以各种策略或预训练模型生成伪训练数据。自行构建的数据集应向组织方开放获取权限。

- **赛道二封闭任务**的参赛队伍需下载组织方预处理后的Lang8数据集和CGED数据集，仅允许采用上述数据进行训练。

- **赛道二开放任务**各参赛队伍可使用各种开源数据进行训练，允许以各种策略或预训练模型生成伪训练数据。自行构建的数据集应向组织方开放获取权限。

- 所有赛道用于训练的数据必须**可开源获取**，并应在论文中说明或以其他方式向比赛组织方公开，**不得使用闭源及私有数据**。

- 所有赛道用于训练的数据必须先使用我们提供的数据剔除程序处理，以防止训练集与开发集、测试集重合。

- 所有赛道和任务仅需创建一个账号，不允许任何队伍以开小号的形式刷榜，参赛队伍之间不允许出现人员交叉。

- 我们会根据大家的反馈，进一步明确或完善规则，请大家关注后续开放的反馈渠道。如果有不明确的地方，务必和我们联系。

- 未遵守上述规定导致结果不可复现的，将取消比赛资格并删除已产生的比赛结果。

## 5. 评价标准

本次评测2个赛道的测试数据集采用封闭方式给出，即仅给定输入文本，需要参赛队伍进行推理预测，并将结果文件打包上传至在线评测平台。平台随后会给出相应赛道的指标得分。每支队伍每天仅可提交3次测试集结果。

### 5.1 赛道一：多维度汉语学习者文本纠错

赛道一所需的结果文件格式是每行对应一个原句的纠正结果。且每个原句仅需提供一个结果。采用的评测指标为基于字的编辑级别的 $F_{0.5}$ 指标。其具体计算步骤如下所示：

1. 我们首先使用基于字的编辑抽取工具抽取出预测编辑集合 $e$ 和正确编辑集合 $g$ ；

2. 然后我们通过如下公式计算 $F_{0.5}$ 指标：

$$P = \frac{TP}{TP + FP} = \frac{| g \cap e |}{| e |}$$

$$R = \frac{TP}{TP + FN} = \frac{| g \cap e |}{| g |}$$

$$F_{0.5} = \frac{(1+0.5^2) \times R \times P}{R + 0.5^2 \times P}$$

其中，\| * \|代表集合内的编辑数目， $\cap$ 代表两个编辑集合的交集。 $F_{0.5}$ 代表更重视精确度，是目前中英文语法纠错最广泛使用的评估指标。

如果当前句子有多种修改方式（假设有 $n$ 种），那么我们对每个修改方式都抽取一个编辑集合，将预测编辑集合与所有正确编辑集合对比，选取尽可能大的 $F_{0.5}$ 指标作为当前句子的指标。

### 5.2 赛道二：中文语法错误检测

赛道二所需的结果文件格式见表2的任务示例。文件每行是对应一个原句的一处检测结果，每行内容为原句的id、错误位置、错误类型及纠正结果。从下述五个方面以精确率、召回率和 $F_{1}$ 值对系统性能进行评价：

1. 假阳性（False Positive）：正确段落单元被判包含错误的比例。

2. 侦测层（Detective-level）：对段落单元是否包含错误做二分判断。

3. 识别层（Identification-level）：本层子任务为多分类问题，即给出错误点的错误类型。

4. 定位层（Position-level）：对错误点的位置和覆盖范围进行判断。错误的边界以词边界界定，分词颗粒度参考jieba缺省模式。

5. 修正层（Correction-level）：参赛系统被要求提交针对错误字符串（S）和字符串缺失（M）两种错误类型的修正答案。每赛题的S和M型错误，均提供1-3个正确答案。参赛队伍可提供1-3个修正结果。精确率和召回率的分子为正规测试集中被命中的答案数量。

## 6. 评测赛程

报名截止时间：2023年5月25日

数据集开放时间：2023年5月1日

提交截止时间：2023年6月1日

结果公布时间：2023年6月10日

| 时间 | 安排 |
|-----| ----- |
| 4 月 15 日 ~ 5 月 25 日 | 开放报名 |
| 4 月 15 日 | 发布数据集 |
| 5 月 7 日 | 参赛系统提交入口开放 |
| 6 月 7 日 | 参赛系统提交入口关闭 |
| 6 月 15 日 | 公布评测结果 |
| 6 月 25 日 | 各参赛队伍截止提交技术报告 |
| 6 月 28 日 | 中英文技术报告反馈 |
| 7 月 3 日 | 正式提交中英文评测论文 |
| 7 月 7 日 | 公布获奖名单 |
| 7 月 10 日 | 评测论文录用通知 |
| 8 月 3 ~ 5 日 | CCL2023 评测研讨会 |

评测网址：http://cuge.baai.ac.cn/

## 7. 奖项设置

本次评测将设置如下奖项：

组委会对获奖参赛单位颁发盖有中国中文信息学会印章的奖状。


## 8. 论文评审

评测委员会将组织专家进行双盲审稿，评测中内容和写作质量均佳的评测报告（中英文）将被收录入 CCL Anthology 和 ACL Anthology。

## 微信交流群

<center>
    <img src="/docs/assets/images/wechat_group.jpg" width="30%">
</center>

**参考文献**

[^1]: Yingying Wang, Cunliang Kong, Liner Yang, Yijun Wang, Xiaorong Lu, Renfen Hu, Shan He, Zhenghao Liu, Yun Chen, Erhong Yang, and Maosong Sun. 2021. YACLC: A Chinese Learner Corpus with Multidimensional Annotation. arXiv preprint arXiv:2112.15043.

[^2]: Yuanyuan Zhao, Nan Jiang, Weiwei Sun, and Xiaojun Wan. 2018. Overview of the NLPCC 2018 shared task: Grammatical error correction. In CCF International Conference on Natural Language Processing and Chinese Computing (NLPCC), pages 439–445.

[^3]: 王莹莹, 孔存良, 杨麟儿, 胡韧奋, 杨尔弘，孙茂松.2023.汉语学习者文本多维标注语料库建设. 语言文字应用,1:88-100

[^4]: 张宝林. 2009. “HSK动态作文语料库”的特色与功能. 汉语国际教育, 4:71–79.

[^5]: Gaoqi Rao, Erhong Yang, and Baolin Zhang. Overview of NLPTEA-2020 Shared Task for Chinese Grammatical Error Diagnosis. In Proceedings of the 6th Workshop on Natural Language Processing Techniques for Educational Applications.
