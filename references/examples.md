# 原创改写示例

这些例子是本技能新写的教学材料，不是目标论文摘录。所有数字均为**纯演示数据**，不能用于用户论文；采用表达时必须换成用户已有且核对过的真实证据。完整动作见 [style.md](style.md)，证据范围见 [prediction-evidence.md](prediction-evidence.md)。以下涉及删除或改变科学主张的改写均是候选修正，须按该文件的科学变更与作者授权规则使用，不作为纯润色中的静默写回示范。

## 1. Results：问题、证据、边界

**演示输入：**冻结测试集含 12 个独立初值轨迹，属于训练分布内二维尾迹；逐轨迹相对速度 L2 再取均值。单步：方法 0.020、基线 0.026；20 步自回归：方法 0.090、基线 0.145。参考为指定数值求解器。只给均值，没有误差带、显著性检验或物理残差。

**粗稿：**
“Our powerful framework accurately captures complex flow dynamics and remains stable for long periods. It comprehensively outperforms the baseline and obeys physical laws.”

**改写：**
“We evaluated prediction error over one-step and autoregressive forecasts on 12 test trajectories with independent initial conditions. The mean relative velocity error was 0.020 for the proposed method and 0.026 for the baseline at one step. At the twentieth autoregressive step, the corresponding errors were 0.090 and 0.145. The proposed method had lower error than the baseline at both evaluated horizons within the tested distribution, with both errors measured against the same reference solver.”

**说明：**S4/S5 将宣传改为问题与证据。保留独立单位、参考及两个时域，不把 20 步终点结果称为整段始终准确、物理守恒或渐近稳定；不添加 p 值或不存在的图号。

## 2. 算子 Methods：输入输出先于模块

**演示输入：**稳态问题；输入为固定位置采样的系数场 a，输出为坐标 x 处的解 u；分支编码采样向量，主干编码 x，内积给标量解值。没有任意传感器迁移测试，没有新定理。

**粗稿：**
“The advanced dual-network architecture learns the entire physics with universal generalization.”

**改写：**
“We approximate the map from the coefficient field to the steady solution. The branch network encodes values of the coefficient field sampled at fixed sensor locations, while the trunk network encodes the output coordinate. Their latent representations are combined by an inner product to predict the solution at that coordinate.”

**说明：**S2 先给数学对象，再给离散输入与组合。不引入时间推进、可变传感器或训练性能保证。真实稿使用他人架构仍需核对并引用方法原文。

## 3. 发现越界主张：区分润色与科学修改

**演示输入：**仅验证集单步相对 L2 为 0.03，未提供测试集或滚动评估。

**粗稿：**
“The model achieves a validation error of 0.03, proving stable and generalizable long-term prediction.”

**候选修正（作者已授权删除无支撑主张时）：**
“The model achieved a one-step relative L2 error of 0.03 on the validation set.”

**说明：**所给材料只支持验证集单步误差，不能据此支持长期稳定和泛化。该候选句删除了实质主张，不得在只要求语言润色时静默写回；按[科学变更边界](prediction-evidence.md#科学变更与作者授权)说明差距及影响，已有相应授权才落实。未提供证据也不等于这些能力已被反证。不索取全套台账或虚构测试。

## 4. 成本：明确测量对象

**演示输入：**相同设备/浮点精度、batch=1、热身后一次 20 步预测纯网络 forward：方法 4 ms、基线 5 ms。不含网格变换、压力求解、I/O 或训练，无等精度求解器计时。

**表述：**
“For a 20-step prediction with batch size one, network evaluation took 4 ms for the method and 5 ms for the baseline under the same hardware and numerical precision. These measurements exclude preprocessing, pressure solves and data transfer.”

**说明：**S3/S5 允许说网络评价更快，不允许说 entire CFD solver is accelerated 或 end-to-end speedup。数据单位一致且用户需要时再算比值，倍率不是必需装饰。

## 5. 其他边界

- “FNO CUDA OOM 怎么修”：属于调试，不进入论文流程，不生成引言或索取图表。
- “尚无结果，先写方法大纲”：依据已有方法写大纲，拟评估项目留在计划中，不填期望性能。
- “按张蒙齐论文逻辑写，但不是控制任务”：采用问题与证据结构，不添加射流、奖励、稳定性分析或控制器。
- “像 FNO 作者写的”：改变定义顺序、论证衔接、术语精度，不复制特征句或增添未提供实验。

## 6. 连续 Methods：从材料到两段正文

**教学输入：**稳态PDE；每个训练样本是系数函数a及其参考解。a在固定的64个传感器处采样，查询点x在定义域内；分支和主干分别产生32维向量，内积输出标量解。训练最小化所提供查询点上的解值MSE。训练/测试按系数函数拆分，测试函数不参与训练。未给网络深度、优化器、样本数、传感器变化实验或定理；不补写它们。

**组织选择：**第一段说明数学对象与可计算接口；第二段说明学习目标与划分单位。它们有定义到使用的联系，不强加物理机制或性能结论。

**正文：**

We approximate the map from a coefficient function to the corresponding steady solution. The coefficient function is sampled at 64 fixed sensor locations and encoded by a branch network. A trunk network encodes the query coordinate. Each network produces a 32-dimensional vector, and their inner product gives the predicted scalar solution value at that coordinate.

Training minimizes the mean squared error between predicted and reference solution values at the supplied query points. The data are split by coefficient function: functions used for testing are excluded from training. The input sensor locations remain fixed.

**核对：**没有将查询点数当独立函数数，没有声称任意传感器适应、时间推进或理论保证。正式Methods仍需作者按重现要求提供训练设置；这不妨碍起草当前授权片段。架构来源按作者真实方法另核引文，不虚构引用键。

## 7. 连续 Results：轨迹、统计与代价各有判断

**教学输入：**相同20条独立初值测试轨迹；A/B第10步相对速度L2均值0.04/0.05，第50步0.20/0.16，均对同一参考求解器计算。100–150 s内平均动能相对参考偏差A/B为1%/3%。同硬件、精度和batch=1，50步纯网络评价耗时6/8 ms，不含预处理、压力求解和传输。无机制检验、显著性或稳定性证明，无图号。

**正文：**

The relative velocity errors of A and B depend on the forecast horizon. Across 20 test trajectories with independent initial conditions, the mean errors at step 10 are 0.04 and 0.05 for A and B, respectively, measured against the same reference solver. At step 50, the corresponding errors are 0.20 and 0.16. A therefore has lower error at step 10, whereas B has lower error at step 50.

The mean kinetic energy over 100–150 s differs from the reference by 1% for A and 3% for B. This statistic favors A despite its larger velocity error at step 50. For a 50-step prediction, network evaluation takes 6 ms for A and 8 ms for B on the same hardware, with the same numerical precision and a batch size of one. The timings exclude preprocessing, pressure solves and data transfer.

**核对与选择：**第一段按时域比较，第二段转到统计与计算对象；这些评价轴并列，不暗示统计一致导致速度提升。保留B的后期优势，未将网络评价扩大为整体CFD加速。若正文需要更多解释，可按统计/计时任务拆第二段；两段不是强制模板。没有统计区间就不补误差带或显著性。

## 8. 无需修改与只审查

有效原文：The spectra agree over the measured wavenumber range, although the trajectories have decorrelated. We report statistical agreement rather than pointwise trajectory accuracy.

若这些事实和术语已定义，原文可保留。although与rather than分别表达两类证据的关系和评价对象的区分，不是假对立；不因去模板腔而删去后半句。仅审查时给判断及必要理由，不主动改文件或要求新实验。
