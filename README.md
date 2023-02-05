光伏短期功率预测大赛
================
李家翔,武睿琦,靳晓松
2023-02-06

<!-- README.md is generated from README.Rmd. Please edit that file -->

# 模型融合

我们尝试的模型融合有

1.  神经网络模型
2.  Xgboost模型
3.  **时间序列模型**
4.  **基于概率模型的融合**

# 结论

本次比赛，我们主要的实现方式是神经网络模型，最终的排名是**52**名。我们的特征工程涵盖了时间相关变量、平方项、立方项、比率、滚动SMA、滚动方差、PCA主成分、实发辐射的测试集预测值、NMF衍生变量、prophet等，而模型融合则涵盖了神经网络模型、Xgboost模型、时间序列模型以及基于概率模型的融合。

# 光伏短期功率预测大赛

这个项目是参加国能日新的[光伏短期功率预测大赛](http://www.dcjingsai.com/common/cmpt/%E5%9B%BD%E8%83%BD%E6%97%A5%E6%96%B0%E5%85%89%E4%BC%8F%E5%8A%9F%E7%8E%87%E9%A2%84%E6%B5%8B%E5%A4%A7%E8%B5%9B_%E7%AB%9E%E8%B5%9B%E4%BF%A1%E6%81%AF.html)的结稿。我们的团队名为
`PHotoVoltaic (phv)`，最终排名是**52**名。

在这个比赛中，我们尝试了一系列的特征工程和模型融合，以提高模型的性能。在特征工程方面，我们加入了时间相关变量、平方项、立方项、比率、滚动SMA、滚动方差、PCA主成分、实发辐射的测试集预测值、NMF衍生变量、prophet等；在模型融合方面，我们尝试了神经网络模型、Xgboost模型、时间序列模型以及基于概率模型的融合。

我们的实现方式主要是神经网络模型，具体见Python代码`wushen.ipynb`，而Xgboost的融合则见R代码`note.Rmd`。我们也使用了`trelliscope`来进行EDA，交互方便，但是不适合上线部署，不便于交流。

最终，我们的模型达到了较好的效果，跑出了**52**名的排名。

![](pic/rank.png)<!-- -->

# EDA

使用`trelliscope`，交互方便，但是不适合上线部署，不便于交流。

1.  [trelliscope/p](https://jiaxiangbu.github.io/phv//trelliscope/p/index.html)
2.  [trelliscope/tsi](https://jiaxiangbu.github.io/phv//trelliscope/tsi/index.html)
3.  [trelliscope/tsi_real](https://jiaxiangbu.github.io/phv//trelliscope/tsi_real/index.html)

# 后续可以做的空间

## 深度学习的方法

1.  可以采用空洞卷积的方法(A. van den Oord et al. 2016a; A. van den Oord
    et al. 2016b; Sprangers, Schelter, and Rijke 2022; Kechyn et al.
    2018)，这种方法可以用于一些其他的应用，比如音频的频谱、长时间序列等。

## XGBoost

1.  由于比赛过程中主办方修改了数据集和评价函数，我们无法复现原来的历史预测，因此，我们没有将神经网络和XGboost进行融合，这也是我们下一次比赛需要注意的问题。
2.  我们可以采用更加合理的窗口特征提取方式(Elsayed et al.
    2021)，以及考虑多任务的框架，如MT-GBT(Ying et al.
    2022)，来提高模型的性能。

## EDA和特征工程

1.  我们需要做好EDA，观察被解释变量关于时间的波动，查看异常值。
2.  在特征工程的部分，为了拟合非线性关系，我们可以使用更高效的Ramsey’s
    RESET test，详见[Github](https://github.com/JiaxiangBU/learn_fe)。
3.  我们也可以参考[预测值迁移](https://jiaxiangbu.github.io/channel_valuation/about)的问题，发现模型可能存在[欠拟合](https://jiaxiangbu.github.io/learn_fe/)的情况，并采取[模型校正部分](https://jiaxiangbu.github.io/train_model/learning_notes.html)的方法来解决。
4.  因为有四个光伏板，并且都是时间序列，所以这里可以采用LSTM训练，参考[6神经网络应用](https://jiaxiangbu.github.io/learn_longitudinal_analysis/analysis/introduction-panel-data.html)。
5.  既然考虑了PCA作为聚类特征，那么应该考虑DTW(Salvador and Chan 2007;
    Izakian, Pedrycz, and Jamal 2015)和TS-PCA(Chang, Guo, and Yao
    2018)。
6.  既然考虑了prophet，那么应该使用prophet的NNs训练(Triebe et al.
    2021)。

------------------------------------------------------------------------

<h4 align="center">
**Code of Conduct**
</h4>
<h6 align="center">
Please note that the ‘phv’ project is released with a [Contributor Code
of Conduct](CODE_OF_CONDUCT.md). By contributing to this project, you
agree to abide by its terms.
</h6>
<h4 align="center">
**License**
</h4>
<h6 align="center">
MIT © [Jiaxiang Li;Ruiqi Wu;Xiaosong Jin](LICENSE.md)
</h6>

<div id="refs" class="references csl-bib-body hanging-indent">

<div id="ref-chang2018principal" class="csl-entry">

Chang, Jinyuan, Bin Guo, and Qiwei Yao. 2018. “Principal Component
Analysis for Second-Order Stationary Vector Time Series.” *The Annals of
Statistics* 46 (5). <https://doi.org/10.1214/17-aos1613>.

</div>

<div id="ref-elsayed2021we" class="csl-entry">

Elsayed, Shereen, Daniela Thyssens, Ahmed Rashed, Hadi Samer Jomaa, and
Lars Schmidt-Thieme. 2021. “Do We Really Need Deep Learning Models for
Time Series Forecasting?” *arXiv Preprint arXiv:2101.02118*.

</div>

<div id="ref-izakian2015fuzzy" class="csl-entry">

Izakian, Hesam, Witold Pedrycz, and Iqbal Jamal. 2015. “Fuzzy Clustering
of Time Series Data Using Dynamic Time Warping Distance.” *Engineering
Applications of Artificial Intelligence* 39: 235–44.

</div>

<div id="ref-kechyn2018sales" class="csl-entry">

Kechyn, Glib, Lucius Yu, Yangguang Zang, and Svyatoslav Kechyn. 2018.
“Sales Forecasting Using WaveNet Within the Framework of the Kaggle
Competition.” *arXiv: Learning*.

</div>

<div id="ref-oord2016wavenet" class="csl-entry">

Oord, Aaron van den, Sander Dieleman, Heiga Zen, Karen Simonyan, Oriol
Vinyals, Alex Graves, Nal Kalchbrenner, Andrew Senior, and Koray
Kavukcuoglu. 2016a. “Wavenet: A Generative Model for Raw Audio.” *arXiv
Preprint arXiv:1609.03499*.

</div>

<div id="ref-oord2016conditional" class="csl-entry">

Oord, Aaron van den, Nal Kalchbrenner, Oriol Vinyals, Lasse Espeholt,
Alex Graves, and Koray Kavukcuoglu. 2016b. “Conditional Image Generation
with PixelCNN Decoders.” *Neural Information Processing Systems*.

</div>

<div id="ref-salvador2007toward" class="csl-entry">

Salvador, Stan, and Philip Chan. 2007. “Toward Accurate Dynamic Time
Warping in Linear Time and Space.” *Intelligent Data Analysis* 11 (5):
561–80.

</div>

<div id="ref-sprangers2022parameter" class="csl-entry">

Sprangers, Olivier, Sebastian Schelter, and Maarten de Rijke. 2022.
“Parameter-Efficient Deep Probabilistic Forecasting.” *International
Journal of Forecasting*.

</div>

<div id="ref-triebe2021neuralprophet" class="csl-entry">

Triebe, Oskar, Hansika Hewamalage, Polina Pilyugina, Nikolay Laptev,
Christoph Bergmeir, and Ram Rajagopal. 2021. “NeuralProphet: Explainable
Forecasting at Scale.” <https://arxiv.org/abs/2111.15397>.

</div>

<div id="ref-ying2022mt" class="csl-entry">

Ying, ZhenZhe, Zhuoer Xu, Weiqiang Wang, and Changhua Meng. 2022.
“MT-GBM: A Multi-Task Gradient Boosting Machine with Shared Decision
Trees.” *arXiv Preprint arXiv:2201.06239*.

</div>

</div>
