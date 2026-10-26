# 来源与文本锚点

初次核查：2026-09-08；PDF 版本与论证细读更新：2026-10-26。J 为控制论文叙事样本，K/F/D 为预测与算子学习的任务参考。编号用于其他技能文件回指，章节和图号以各卡明确的版本为准。

本文件记录的是所列文本的结构分析，**不是数学正确性审计、统计意义上的作者风格画像，也不是作者个人身份证明**。直接观察与技能中的综合编辑建议分开；不复制长句，不移植来源论文的实验数值、性能结论、参数或适用范围。阅读过理论段落不等于验证证明；参考文献中的结论不能替代用户研究的证据。

## PDF 归档与版本对应

四份分析所用 PDF 可按 [assets 文件名与许可说明](../assets/README.md)在本地归档。公开仓库仅随附 J 的 CC BY-NC-SA 4.0 版本，其余三篇使用原文链接；本地阅读副本不纳入 Git。准确版次以下表和 PDF 首页为准。J 的副本不含私人阅读批注，正文和分页保持原版。逐篇细读链接内包含完整结构地图、段落推进、代表性逐句分析及具体覆盖说明。

| 来源 | 阅读入口 | 实际版本与页数 | 原文细读 |
| --- | --- | --- | --- |
| J | [Li-Zhang-2022-JFM.pdf](../assets/Li-Zhang-2022-JFM.pdf) | arXiv:2111.07498v1，2021-11-15，35页，公开原件，无私人批注；不是 JFM 最终排版 | [Li–Zhang](paper-analyses/li-zhang.md) |
| K | [arXiv v1 PDF](https://arxiv.org/pdf/2102.01010v1) | arXiv:2102.01010v1，首页标记2021-01-28，13页，正文和附录合并；不是 PNAS 排版 | [Kochkov](paper-analyses/kochkov.md) |
| F | [arXiv v3 PDF](https://arxiv.org/pdf/2010.08895v3) | arXiv:2010.08895v3，2021-05-17，16页，首页标 ICLR 2021 | [FNO](paper-analyses/fno.md) |
| D | [五作者期刊版入口](https://doi.org/10.1038/s42256-021-00302-5) | 五作者 NMI 排版版，15页；文章218–229加3页Reporting Summary | [DeepONet](paper-analyses/deeponet.md) |

K 归档采用作者稿，细读以该版为主，并另列与正式版的结构差异，不只替换页码。四份均经PDF解析确认身份和页数；代表性细读按PDF版面核对段界。无需再次下载才能使用技能。

## J：物理问题驱动与条件化检验

Jichao Li and Mengqi Zhang. **Reinforcement-learning-based control of confined cylinder wakes with stability analyses.** *Journal of Fluid Mechanics* **932**, A44 (2022). [DOI: 10.1017/jfm.2021.1045](https://doi.org/10.1017/jfm.2021.1045)；[arXiv:2111.07498](https://arxiv.org/abs/2111.07498)。Cambridge 在线日期为 2021-12-14，卷期日期为 2022-02-10。

- 实际阅读版本：表中归档 arXiv v1 PDF，未证明其与最终发表稿逐字一致。正式书目为 **932 / A44**。
- 阅读覆盖：摘要、正文全部小节及附录论证职责；四个自然段逐句细读，含引言、方法、结果与收束；范围详见逐篇文件。§5.3 在 PDF 中是一个自然段，自动转录的拆段不能代替原文分段。以下锚点已回归档 PDF 核查；未完成公式、代码或证明审计。

| 编号 | 文本锚点 | 精炼直接观察 |
| --- | --- | --- |
| J1 | Abstract；§1.1–1.3 | 物理问题与机器学习两条背景线收束到研究问题。 |
| J2 | §2；§3.1–3.2 | 先交代标度和求解方法，并区分基流与平均流。 |
| J3 | §4.3–4.4；Figs. 7–10 | 分析结果衔接后续控制设计。 |
| J4 | §5.3；Fig. 14 | 改变启动相位构成条件对照。 |
| J5 | §5.4–5.6；Figs. 15–21 | 常值替换、模式、扰动及观测布置承担不同检验功能。 |
| J6 | §6.1–6.2 | 分别总结物理与控制认识，并保留范围条件。 |

## K：数值结构、学习部件与精度—成本关系

Dmitrii Kochkov, Jamie A. Smith, Ayya Alieva, Qing Wang, Michael P. Brenner, and Stephan Hoyer. **Machine learning–accelerated computational fluid dynamics.** *Proceedings of the National Academy of Sciences* **118**(21), e2101784118 (2021). [DOI: 10.1073/pnas.2101784118](https://doi.org/10.1073/pnas.2101784118)。

- 实际阅读版本：初次核读 [PMC 保存的 PNAS 发表全文](https://pmc.ncbi.nlm.nih.gov/articles/PMC8166023/)，PMCID PMC8166023；本次详细分析和归档依据 [arXiv v1](https://arxiv.org/abs/2102.01010v1)，并对照 [PNAS 正式版](https://www.pnas.org/doi/pdf/10.1073/pnas.2101784118)可读文本。[Crossmark](https://crossmark.crossref.org/dialog?cm_version=v2.0&doi=10.1073/pnas.2101784118&domain=www.pnas.org)记录正式版本自2021-05-18生效，卷期日期2021-05-25。
- 版本差异：[Google Research 书目页](https://research.google/pubs/machine-learning-accelerated-computational-fluid-dynamics/)摘要数值范围与发表版不同；正式书目以 DOI 为准，以下文本组织锚点以归档作者稿为准，不从书目页移用性能数字。
- 阅读覆盖：作者稿 Abstract、正文I–IV全部小节、Figs.1–6和附录A–G的论证职责；五个代表自然段逐句细读。作者稿的方法在II.B，正式版另设Methods，句数也有变化。以下锚点以归档版为准；Significance/Data Availability是正式版额外内容，不冒充归档内容。未核验作者代码或数学正确性。

| 编号 | 文本锚点 | 精炼直接观察 |
| --- | --- | --- |
| K1 | Abstract；I Introduction；Fig.1a–c | 由计算瓶颈进入方法，并限定二维流动范围。 |
| K2 | II.A Navier–Stokes；II.B Learned solvers | 学习近似与保留数值结构分工说明。 |
| K3 | II.B.1 Learned interpolation / II.B.2 Learned correction | 插值系数与残差修正分开命名、说明。 |
| K4 | II.B.3 Training；未编号损失公式周围 | 粗化参考轨迹与模型递推共同进入训练说明；正式版对应Eq.2。 |
| K5 | III.A.1 Accuracy；Fig.2a–c | 场图、轨迹相关性与去相关后能谱分工明确。 |
| K6 | III.A.2 Computational efficiency；Fig.1a；Appendix F | 加速围绕同等精度，并交代开销；总图大域精度含外推，非全部直接测量。 |
| K7 | III.A.3 Generalization；III.B Comparison to other ML models；Figs.3–5 | 条件逐项改变，指标与横向设计比较各有职责。 |
| K8 | III.C Acceleration of LES；Fig.6；IV Discussion Eq.2 | LES重置参考对象；三维收益为外推讨论。正式版成本式为Eq.3。 |

## F：函数映射、架构与条件化实验

Zongyi Li, Nikola Kovachki, Kamyar Azizzadenesheli, Burigede Liu, Kaushik Bhattacharya, Andrew Stuart, and Anima Anandkumar. **Fourier Neural Operator for Parametric Partial Differential Equations.** ICLR 2021. [OpenReview 入口](https://openreview.net/forum?id=c8P9NQVtmnO)。

- 实际阅读版本：[作者 arXiv v3 PDF](https://arxiv.org/pdf/2010.08895v3)，2021-05-17 修订，16 页，首页标明 ICLR 2021；[版本记录](https://arxiv.org/abs/2010.08895v3)。阅读范围不包括 OpenReview 讨论区，未逐字比较不同版本。
- 阅读覆盖：摘要、正文§1–6全部层级与段落/段群推进，六个代表自然段逐句细读；附录只分析分工。§6是条件与延伸设想的收束，不是标准化结果复述。页码取归档v3；未审计全部文献、附录证明或源码。

| 编号 | 文本锚点 | 精炼直接观察 |
| --- | --- | --- |
| F1 | Abstract；§1–2 | 重复求解需求收束到函数映射，贡献按能力分项。 |
| F2 | §3；Fig. 2 | 先展示整体架构，再解释分支及其连接。 |
| F3 | §4 | 频域计算对应明确的实现操作。 |
| F4 | §5.1–5.5；Fig. 3；Table 1；Fig. 6 | 同网格、跨网格与下游任务分别呈现比较条件。 |

## D：理论启发、数据组织与分层证据

Lu Lu, Pengzhan Jin, Guofei Pang, Zhongqiang Zhang, and George Em Karniadakis. **Learning nonlinear operators via DeepONet based on the universal approximation theorem of operators.** *Nature Machine Intelligence* **3**, 218–229 (2021). [DOI: 10.1038/s42256-021-00302-5](https://doi.org/10.1038/s42256-021-00302-5)，正式发表日期为 2021-03-18。

- [期刊页面](https://www.nature.com/articles/s42256-021-00302-5)核对书目；正文核读来源包括 [Lu Lu 上传的排版全文](https://www.researchgate.net/publication/350158010_Learning_nonlinear_operators_via_DeepONet_based_on_the_universal_approximation_theorem_of_operators)网页文本与归档的五作者排版 PDF。亦核对了 [公开教学副本](https://aiichironakano.github.io/cs653/Lu-DeepONet-NMachineIntell21.pdf)的相同题名、DOI、作者与页数，未宣称对两个副本逐字比较。
- 阅读覆盖：摘要、引言、理论/架构/数据、Results全部命名小节、结论及Figs.1–6；四个代表自然段逐句细读；正文218–227页版面已核对。未逐条验证补充证明或执行代码；归档末三页Reporting Summary不能误称补充证明。
- 版本隔离：[arXiv:1910.03193v3](https://arxiv.org/abs/1910.03193v3)为 2020-04-15 三作者预印本，作者 Lu Lu、Pengzhan Jin、George Em Karniadakis，题名 **DeepONet: Learning nonlinear operators for identifying differential equations based on the universal approximation theorem of operators**。本卡锚点只使用上述五作者期刊版本，不共用预印本图号。

| 编号 | 文本锚点 | 精炼直接观察 |
| --- | --- | --- |
| D1 | 引言；Fig. 1 | 输入函数与输出查询位置的角色分开定义。 |
| D2 | p. 220 理论段 | 逼近、优化与泛化误差分开讨论。 |
| D3 | 架构及 Data generation，pp. 220–222 | 架构连接信息角色，数据说明区分函数数与查询数。 |
| D4 | Results and discussion；Figs. 2–6；Conclusions，pp. 222–227 | 算子类别、数据规模及输入分布变化各有结果锚点。 |

## 使用边界

这些卡支持文本组织判断；跨来源形成的写作规则属于技能的原创综合建议。理论保证、算法能力、实际实现和实测表现仍须逐项核验。尤其不能互换轨迹精度与统计精度、可查询坐标与未来时间外推、跨网格评估与跨工况泛化，以及参考求解器一致性与真实物理验证。
