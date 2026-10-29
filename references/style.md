# 四源合成的写作决策

以下是**综合建议**，不是四篇文章共同宣告的标准，也不是作者习惯的统计画像。J/K/F/D 是 [sources.md](sources.md)中已核读的章节锚点。以当前论文实际贡献选择主线；样本的期刊结构、强烈措辞和实验结果不自动迁移。

本页侧重写作取舍与语言。需要理解作者如何及为何组织章节、自然段和句子时，读 [argument-architecture.md](argument-architecture.md)及其四份原文细读；本页原创例句不作为原文细读证据。

## 先选主线

| 真正贡献 | 主线 | 避免的错配 |
| --- | --- | --- |
| 物理认识解释或指导预测设计 | J：现象/问题 → 物理分析 → 设计选择 → 独立检验 | 流场外观相似被写成已发现机制；强制加入 RL、DMD 或控制实验 |
| 数值模拟或混合求解器加速 | K：计算瓶颈 → 被学习的数值近似 → 保留结构 → 精度与成本 | 局部网络推断被写成整体求解器加速 |
| 新的算子或场映射表示 | F/D：函数映射 → 表示/结构 → 离散实现 → 误差与范围 | 通用逼近被写成训练成功、稳定性或跨几何泛化保证 |

没有物理机制贡献就直接写方法与预测证据，不为贴近 JFM 强造物理解释。静态 PDE 参数到解映射不必写自回归 rollout。

## S1：由科学问题收束到可检验目标

**场景：**引言只有领域热度、应用清单或“现有方法不足”。

**动作：**先交代具体系统与预测需求，再指出要处理的物理/计算关系；按这条关系组织文献，最后说明本研究实际改变哪一环。依据 J1 的问题定位和 K1 的计算瓶颈开题。面向同行可更快进入问题，面向跨学科读者先解释其后果。

**原创示例（相应困难已有证据时）：**
“Long-horizon wake prediction requires the phase of vortex shedding to remain consistent over repeated updates. We examine how the treatment of boundary information affects this accumulated error.”

**边界：**不得凭模型名称捏造困难；研究问题不等于已经证实边界信息是误差原因。样本的历史 novelty 声明不支持当前“首次”。

## S2：先定义映射，再解释网络

**场景：**Methods 从网络层数和模块名开始，输入输出的科学含义不清楚。

**动作：**按 F1–F3 / D1–D3，在读者需要理解网络操作时，明确输入函数、条件参数、输出对象和求值位置，并说明采样、编码、组合和训练。可从映射定义或架构概览切入，已有定义直接回指。用真实数据流串起公式与实现，不把理论算子和某一网格张量混为一谈。

**原创示例（用户方法如此时）：**
“The predictor maps an observed velocity history to the velocity field at the next time level. The history is sampled on the computational grid before it is passed to the learned map.”

**边界：**固定传感器输入不等于任意传感器位置通用；可在新坐标求值不等于已证实分辨率无关精度。不给普通回归器附加未实现的算子属性。

## S3：让保留结构和学习修改各有所指

**场景：**“融合物理和数据”“学习复杂动力学”代替方法说明。

**动作：**按 K2–K4 / J2，写清一次更新中保留、学习、训练后固定、后处理的部分，各自操作的变量和执行顺序。约束的设计动机、数学保证、实测效果分别表达。

**原创示例（实现支持时）：**
“The network predicts a correction to the provisional velocity. The corrected field is then passed to the pressure-projection step.”

**边界：**这两句不证明离散散度或边界误差为零；无结构分析或残差证据，不添加 exactly conservative / divergence-free。也不把后处理描述成训练耦合。

## S4：用明确对照回答一个问题

**场景：**Results 逐张介绍图，却没有比较目的。

**动作：**借鉴 J3–J5 的“改变条件以检验解释”。明确对照改变了什么、观察到什么及回答了哪个问题；可先给条件，也可先给发现后紧接必要条件，不要求每段按三步展开。只使用已完成对照，列出额外检验需求不等于授权执行。

**原创示例（已有相应对照时）：**
“We next vary the initial shedding phase while keeping the trained predictor fixed. This comparison tests whether the observed error depends on the phase at which prediction begins.”

**边界：**相位对照不支持跨 Reynolds 数鲁棒；仅观察相关变化时，说明关联或待检验解释，不直接认定因果。

## S5：让证据类型决定性能句

**场景：**“accurate, stable and efficient”掩盖不同指标。

**动作：**按 K5–K8、F4，将轨迹误差、统计重现、运行不发散、成本分别叙述；在读者判断结果所需的位置明确比较口径，共享条件可统一交代，后续不必逐句重复；按实际关系并列或连接。图注说明各面板测量什么。

**原创示例（用户结果支持时）：**
“The predicted spectrum retains the reference distribution after the trajectories decorrelate. This agreement concerns the sampled statistics rather than the phase of individual vortices.”

**边界：**不挪用样本倍率、时域和阈值。与教师求解器一致不等于与物理真值完全一致；同等网格、同等误差、同等预算是不同对照。

**表述取舍：**正文用明确的测量对象和范围限定结论，不默认每段追加“这些结果不能证明……”式审核说明。未测维度可在给用户的说明中列出；已完成的不利比较和理解结果所需的条件必须留在正文，不能一起移走。

## S6：先确定结论强度，再选动词

**场景：**逼近定理、机制解释和数值结果都使用同样强的结论。

**动作：**参照 D2/D4 和 J5/J6，写出每项结论的依据。定义和推导用现在时；已完成实验多用过去时，图表呈现的关系可用现在时。保持全文体例一致，不机械切换时态。

**原创示例：**
“The representation is motivated by operator approximation theory. Its prediction accuracy is evaluated separately on the stated test distribution.”

**边界：**show 可用于明确观察；suggest / may 用于间接解释，但降调词不会补足不存在的证据。没有证明不使用 guarantee；没有相应检验不使用 statistically significant。

## 语言层：科学对象与关系

依据是 J1–J6 的问题承接和图证说明、K2–K7 的操作/指标命名、F1–F4 和 D1–D4 的定义到实测转移。以下是编辑建议，未测量句长或词频。

- 用 wake、velocity field、solution operator、prediction error 等已定义对象作主语，避免连续多句 The proposed framework 开头。
- 使用 maps、approximates、updates、projects、decreases、matches 等具体动作，不用多层名词堆叠掩盖动作。
- 对比句说明相对谁、哪个条件、哪个量怎样变化，不靠 superior、remarkable、powerful、highly robust 表态。
- 后段可承接前段问题，也可引入并列评价、必要设置或新范围；逻辑确有转折或后果时才加连接词，不每段轮流 Moreover / Furthermore / Importantly。
- 保留符号和术语，不为词汇变化将 prediction、reconstruction、simulation、control 互换。
- 第一人称用于研究选择，物理对象用于现象，必要被动语态用于操作。不模仿语法瑕疵、硬凑口头禅或强制单一语态。
- 引文描述真实贡献与条件。思想或方法借用需准确引用；一般论证技巧不要求每段机械插入四篇风格来源。

辅助设计参考了 ARS 的软性风格校准与 claim–evidence 连接、Nature 写作/润色的段落功能及术语一致性。四源具体风格优先；未继承固定句长、强制双语、固定章节或每次确认流程。

## ARS 六维风格软校准

采用ARS-Codex 3.23.2的`ars/shared/style_calibration_protocol.md`所提供的六维观察，按本skill的四源任务适配；来源分工与语言复核见[联合指南](ars-writing-quality.md)。这是本地原则提炼，不是执行完整ARS流程或创建强制风格画像文件。

| 维度 | 如何观察与使用 | 不机械迁移什么 |
|---|---|---|
| 句子节奏 | 看短句怎样定位判断、长句怎样承载条件与关系，按信息量调整 | 未测量的均值/比例、固定长短交替 |
| 段落长度 | 看一个自然段完成什么工作，是否需要多步支撑 | 固定句数、每个动作单独一段、照搬网页换行 |
| 词汇与动词 | 保持对象稳定，区分定义、观察、解释及证明 | 为匹配作者而升级suggest为demonstrate，或轮换专业术语 |
| 引文整合 | 关键来源如何进入问题/设计/解释，旁证如何简洁归属 | 固定引用密度、未核读的样本文献引用链 |
| 修饰语 | 具体量和条件如何承担强调，哪些修饰具有实际判断作用 | 机械删除robust等技术用语，或仿写强优先权声明 |
| 章节语气 | 方法解释操作，结果呈现比较，讨论综合意义；按当前期刊调整 | 声称某期刊一律短段、某学科只能主动或第三人称 |

先按当前任务选相近来源段，再提炼可解释的写作选择，应用到自己的科学对象；完成后检查含义和阅读效果，不评作者相似度。四篇合著样本提供文章层面的观察，不能合成为某位作者的个人画像。用户明确要求个人风格时，只对其确认执笔的材料作判断；单篇或异语言样本只迁移可支持的维度，不为普通对标任务强索三篇样本。

风格服从真实含义、用户范围和适用投稿规范。样本句序是选择，不是缺陷判据；有效写法允许保留。普通任务无需另交画像报告。交付前应用ARS表达诊断和Humanizer结构复核；不为了仿写保留样本中的空话，也不为了去模板腔删除有作用的定义、限定和总结。
