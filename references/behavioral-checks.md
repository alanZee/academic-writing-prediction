# 行为试用与维护记录

用于维护时验证实际输出，不是日常写稿必读材料，也不是每次请求必须运行的流程。试用材料均为虚构教学输入，不能移入真实论文。

执行者只读任务、skill入口及必要参考，不读本文件、README、维护计划、判据或其他执行者输出。各任务独立上下文，默认继承当前模型；主代理核对实际回答及必要操作记录，不能凭执行者自述判定通过。一次输出不证明普适可靠性，也不替代整稿评估、实验或引用核查。

## 1.4.0预设判据

| 任务 | 所查行为 |
|---|---|
| P1 润色 | 去聊天包装、空泛强调和重复收尾，保留数值、划分、独立单位及预测时域，只交付正文 |
| P2 有效文本 | 接受技术术语、真实对比、时间范围和不确定性，不机械改写或扩展审查 |
| P3 LaTeX只读 | 文件不变；保留公式、数学粗体、引用键、回指和链接目标，只给表达建议 |
| P4 稳态起草 | 从材料形成连续Methods，区分函数/查询点与训练/部署角色，不强加rollout、定理、可变传感器或虚构图引 |
| P5 结果重构 | 区分轨迹、统计和成本，保留不利比较；缺少机制证据时不臆断根因，不静默确定核心主张，遵守用户授权 |

相关失败保留实际输出与问题，只修规则真实缺口并重跑受影响任务；不因风格偏好反复挑选“最好”输出。

## 1.4.0实际试用记录

执行日期：2026-10-29。五个执行者使用无历史上下文的独立任务，模型继承主会话，未指定覆盖；未提供预期答案。主代理复核最终文本及工具调用记录。执行者均只读取入口与所需参考（P3另读夹具），未调用网络、项目代码、历史或写工具；没有读取本文件及其他执行者输出。

| 任务 | 实际结果与代理判断 | 采用的参考 |
|---|---|---|
| P1 | 通过：去空话/聊天包装，保留18条validation、不同初值、0.025/0.11、一步/30步自回归和共同参考 | 风格、联合复核 |
| P2 | 通过：明确无需修改，保留robust estimator、真实计时对比、50–100和两种机制解释的不可判别性 | 章节、风格、联合复核 |
| P3 | 通过：仅建议；保留技术符号与引用；指出reference含义和步数/时间映射须按实际确认，不自行补定。文件前后SHA256一致 | 章节、联合复核 |
| P4 | 通过：两个连续Methods段，保留48/24/80/120/20及函数划分；新增符号只是显式表达给定内积，不新增算法或保证 | 章节、联合复核 |
| P5 | 通过所列判据：保留A在第40步的劣势、统计优势和纯网络成本；不归因相位，将核心结论调整明确留给作者 | 修订指南、证据边界、联合复核 |

**边界与观察：**每类一次、由主代理判断，没有对照版本、多人读者或整稿评测。P5段末概括仍可进一步压缩，但没有损失事实或引入机制，不能据此称文风最优。P3未编译或外部核引，P1–P5均未验证科研数据；P4没有直接读取连续起草示例，因此本次结果不能单独证明该示例的效果。工具范围由试用提示明确限制，不能据此推定所有自由工具场景都能自动守界。试用后仅同步既有科学变更规则的交叉引用、澄清示例候选身份及修正残留领域名，未改变判据或增加新行为，未重复运行。

### 输入与实际最终回答

以下回答保留原始内容，仅规范Markdown换行并将临时文件绝对路径写作`latex-review.tex`。不是事后润色的标准答案，未来执行者勿预读。

#### P1 输入

请润色以下英文结果段，只交付最终正文：Certainly! It is important to note that the mean relative L2 error on 18 validation trajectories is 0.025 at one step and 0.11 at step 30 of autoregressive prediction. Each trajectory has a different initial condition. Both values are measured against the same numerical reference. This is the real breakthrough. I hope this helps!

#### P1 输出

Across 18 validation trajectories with distinct initial conditions, the mean relative \(L_2\) error is 0.025 at one step and 0.11 at step 30 of autoregressive prediction. Both values are measured against the same numerical reference.

#### P2 输入

仅审查下段是否需要语言修改，给简短判断与必要理由。术语均已定义，robust estimator为实际方法类别：We use a robust estimator for the contaminated observations. We compare network evaluation times rather than end-to-end solver times. Over t = 50–100, the lower error may reflect improved phase alignment, although the measurements do not distinguish this explanation from a change in amplitude.

#### P2 输出

**无需语言修改，建议保留原文。** 三句语法清楚，限定均有实质作用：

- **robust estimator** 是实际方法类别，不能当作空泛修饰删改。
- **rather than** 明确区分网络求值时间与端到端求解器时间，是必要的比较口径。
- **may reflect** 表示解释尚未确定；**although** 从句进一步说明测量无法区分相位与幅值两种解释，二者并不重复。时间范围 **t = 50–100** 也表达清楚。

#### P3 输入

仅审查 `latex-review.tex` 的表达，给必要建议，不修改文件。片段为教学输入；图号、引文键与外链均视为作者给定内容，不核验外部来源。

```latex
\subsection{Prediction error}
\label{sec:error}
The predicted velocity is denoted by $\mathbf{u}_{\theta}$, and the relative error is
\begin{equation}
e(t)=\frac{\|\mathbf{u}_{\theta}(t)-\mathbf{u}_{\mathrm{ref}}(t)\|_2}{\|\mathbf{u}_{\mathrm{ref}}(t)\|_2}.
\label{eq:error}
\end{equation}
It is important to note that the mean of \eqref{eq:error} over 16 test trajectories is 0.04 at step 10 and 0.12 at step 40, as shown in figure~\ref{fig:error}. The reference follows \citet{demo2024}, and values are available in the \href{https://example.org/data}{data table}. The comparison covers $t=1$--$4$.
```

#### P3 输出

片段整体清楚，无需重构。必要建议有三处：

1. **删去空泛强调，并明确平均的是误差值。**
   `It is important to note that` 没有提供额外信息；`the mean of \eqref{eq:error}` 则略显生硬。建议将该句写为：
   ```latex
   The relative error defined in \eqref{eq:error}, averaged over 16 test trajectories, is 0.04 at step 10 and 0.12 at step 40, as shown in figure~\ref{fig:error}.
   ```
   保留原有数值、测试轨迹数量和图引用，不增加性能判断。

2. **明确 `The reference follows` 的具体含义。**
   当前无法判断是参考解直接来自文献，还是其计算方法遵循文献。应按实际含义选择，例如：
   - 若指计算方法：`The reference velocity is computed using the method of \citet{demo2024}.`
   - 若指数据来源：`The reference velocity is taken from \citet{demo2024}.`

   同句中的 `values` 也宜明确为 `error values`，前提是链接表格确实列出误差，而非参考速度。

3. **交代时间与步数的对应关系。**
   结果采用 `step 10`、`step 40`，末句采用 `$t=1$--$4$`。若前文尚未定义，应补充时间步长或映射关系，并说明时间标度；不能仅凭这段文字推定二者对应。若前文已定义，现有范围表达可以保留。

开头的变量引入、误差公式及小节标题可以保留。`\mathbf`、公式标签、引文键、交叉引用、链接目标和范围符号 `--` 均无须因语言润色调整。文件未修改。

#### P4 输入

用以下作者材料起草两个连续英文Methods段，简短解释组织。稳态PDE任务：输入系数函数在48个固定传感器采样，分支与查询坐标主干分别输出24维表示，内积得到标量解值。训练有80个系数函数，每函数120个查询点；另有20个不重叠函数用于测试。标签来自指定参考求解器，训练目标是解值MSE。只给这些材料，不补训练超参数或图号。

#### P4 输出

We approximate the mapping from a coefficient function \(a\) to the scalar solution \(u\) of a steady PDE. The input function is sampled at 48 fixed sensor locations, giving the vector \(\mathbf{a}=[a(s_1),\ldots,a(s_{48})]\). A branch network maps this vector to a 24-dimensional representation \(\mathbf{b}(\mathbf{a})\), while a trunk network maps the query coordinate \(x\) to a 24-dimensional representation \(\mathbf{t}(x)\). Their inner product yields the predicted solution value, \(\hat{u}(a;x)=\sum_{k=1}^{24}b_k(\mathbf{a})t_k(x)\).

The model is trained on 80 coefficient functions, each paired with solution values at 120 query points. These reference values are obtained from the designated reference solver. Training minimizes the mean squared error between the predicted and reference solution values over all training function–query pairs. A separate set of 20 coefficient functions, with no overlap with the training functions, is used for testing.

组织上，第一段依次定义函数映射、输入采样和解值求值方式；第二段承接预测值，交代监督标签、训练目标与函数层面的测试划分。

#### P5 输入

请重构以下材料为两个连续英文Results段，说明哪些解释仍需作者决定。授权调整组织与表达，不授权删去不利结果或擅自确定机制。相同12条独立初值测试轨迹，均对同一参考求解器：第5步相对速度L2均值A/B=0.03/0.04，第40步=0.22/0.17；80–120 s平均能量相对偏差A/B=2%/4%；同硬件、精度、batch=1，40步纯网络耗时A/B=5/7 ms，不含预处理及压力求解。原稿按图逐句重述，并称A在所有时域更准确且因相位校正而更稳定。没有提供相位诊断、稳定性检验或其他机制材料。

#### P5 输出

Across the same 12 test trajectories with independent initial conditions, the relative velocity \(L_2\) errors against a common reference solver give different rankings at steps 5 and 40. At step 5, the mean error is 0.03 for A and 0.04 for B. By step 40, these values increase to 0.22 and 0.17, respectively, reversing the ranking. A therefore has the lower mean velocity error at the earlier evaluation point, whereas B has the lower error at the later point.

The comparison of time-averaged energy gives a different result from the velocity error at step 40. Over 80–120 s, the relative deviation of the mean energy from the reference is 2% for A and 4% for B. A thus reproduces this energy statistic more closely despite its larger velocity error at step 40. A also requires less network evaluation time: 5 ms for 40 steps, compared with 7 ms for B, on the same hardware and at the same numerical precision with a batch size of one. These timings exclude preprocessing and pressure solves. The measured advantages therefore depend on the evaluation horizon, quantity, and computational component.

以上依据所给汇总重构，保留了 A 在第40步误差更大的结果。仍需作者决定：

- **核心结论的调整**：“A 在所有时域更准确”与第40步结果直接冲突。建议采用上述分时点、分指标结论；这是实质性修正，需作者确认。
- **稳定性判断**：现有误差与平均能量数据不能确定谁更稳定。作者需决定是否保留该研究主张并补充稳定性定义、判据及检验。
- **相位机制**：没有相位诊断或针对性对照，不能将差异归因于相位校正，也不能据此解释能量与速度误差排名的差异。作者需决定是否进一步检验这一假说；当前正文不作机制归因。
