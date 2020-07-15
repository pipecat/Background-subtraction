# 完成

- vibe测试
    - 测试纯色衣服时身体的前景背景判断
    - 测试人物走动中的背景判断
- 跑通BiSeNet_V2的开源实现 [https://github.com/CoinCheung/BiSeNet]
(https://github.com/CoinCheung/BiSeNet)<br>
    BiSeNet_V2论文：[https://arxiv.org/pdf/2004.02147.pdf](https://arxiv.org/pdf/2004.02147.pdf)<br>
    效果：test_01.jpg -> res.jpg(更改数据集后可能改善)
- 实时语义分割（Semantic segmentation） -> 实时人像分割（Portrait segmentation）<br>
    把 Real time semantic segmentatio 的问题细化到 Real time portrait segmentation 上，找到了相关论文与项目
    - [https://github.com/lizhengwei1992/Fast_Portrait_Segmentation](https://github.com/lizhengwei1992/Fast_Portrait_Segmentation)  实时转化为黑白背景
    - [https://github.com/anilsathyan7/Portrait-Segmentation](https://github.com/anilsathyan7/Portrait-Segmentation) 实时人像分割
    - [https://arxiv.org/pdf/1911.09099v4.pdf](https://arxiv.org/pdf/1911.09099v4.pdf) PortraitNet
    - [https://github.com/clovaai/ext_portrait_segmentation](https://github.com/clovaai/ext_portrait_segmentation),[https://arxiv.org/pdf/1908.03093.pdf](https://arxiv.org/pdf/1908.03093.pdf) ExtremeC3Net,运算量为PortraiNet的三分之一左右（官方开源）
- 人像数据集
    - [https://www.kaggle.com/laurentmih/aisegmentcom-matting-human-datasets](https://www.kaggle.com/laurentmih/aisegmentcom-matting-human-datasets)
    - [https://rapidapi.com/etcloud-etcloud-default/api/portrait-img-segmentation](https://rapidapi.com/etcloud-etcloud-default/api/portrait-img-segmentation)
# 待完成
- 对已经跑通的项目，进行测试集的更换，然后测试效果与性能
- 在已找出的方案与开源实现中尽量做到跑通并测试，并对不同方案结果进行对比
- 继续对项目，论文进行调研，寻找最适合我们应用场景的方案
- 对深度学习基础知识进行学习