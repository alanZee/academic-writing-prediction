# 原创改写示例

这些例子是本技能新写的教学材料，不是目标论文摘录。所有数字均为**纯演示数据**，不能用于用户论文；采用表达时必须换成用户已有且核对过的真实证据。完整动作见 [style.md](style.md)，证据范围见 [prediction-evidence.md](prediction-evidence.md)。

## 1. Results：问题、证据、边界

**演示输入：**冻结测试集含 12 个独立初值轨迹，属于训练分布内二维尾迹；逐轨迹相对速度 L2 再取均值。单步：方法 0.020、基线 0.026；20 步自回归：方法 0.090、基线 0.145。参考为指定数值求解器。只给均值，没有误差带、显著性检验或物理残差。

**粗稿：**
“Our powerful framework accurately captures complex flow dynamics and remains stable for long periods. It comprehensively outperforms the baseline and obeys physical laws.”

**改写：**
“We evaluated prediction error over one-step and autoregressive forecasts on 12 test trajectories with independent initial conditions. The mean relative velocity error was 0.020 for the proposed method and 0.026 for the baseline at one step. At the twentieth autoregressive step, the corresponding errors were 0.090 and 0.145. The method therefore reduced error relative to the reference solver at both evaluated horizons within the tested distribution.”

**说明：**S4/S5 将宣传改为问题与证据。保留独立单位、参考及两个时域，不把 20 步终点结果称为整段始终准确、物理守恒或渐近稳定；不添加 p 值或不存在的图号。

## 2. 算子 Methods：输入输出先于模块

**演示输入：**稳态问题；输入为固定位置采样的系数场 a，输出为坐标 x 处的解 u；分支编码采样向量，主干编码 x，内积给标量解值。没有任意传感器迁移测试，没有新定理。

**粗稿：**
“The advanced dual-network architecture learns the entire physics with universal generalization.”

**改写：**
“We approximate the map from the coefficient field to the steady solution. The branch network encodes values of the coefficient field sampled at fixed sensor locations, while the trunk network encodes the output coordinate. Their latent representations are combined by an inner product to predict the solution at that coordinate.”

**说明：**S2 先给数学对象，再给离散输入与组合。不引入时间推进、可变传感器或训练性能保证。真实稿使用他人架构仍需核对并引用方法原文。

## 3. 一句润色：不升级证据

**演示输入：**仅验证集单步相对 L2 为 0.03，未提供测试集或滚动评估。

**粗稿：**
“The model achieves a validation error of 0.03, proving stable and generalizable long-term prediction.”

**改写：**
“The model achieved a one-step relative L2 error of 0.03 on the validation set.”

**说明：**保留事实；长期稳定及泛化无证据，故删除。完成句子，不索取全套实验账本或虚构测试。

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
