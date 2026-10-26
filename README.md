# 学术写作-小论文-预测任务

面向科学机器学习、CFD/PDE、神经算子和动力系统预测论文的 Codex 用户级 skill。技术名称：`academic-writing-prediction`。

主要辅助手稿的**规划与撰写**，也支持**审查、优化、重构、润色和学术中译英**。这些工作共用一个基础：明确这篇手稿该是什么样，以及该怎么写；再对照现有材料，完成当前需要的规划、写作或修改。

从科学问题与知识目标出发，自顶而下设计论证、实验与判定标准；从实际证据出发，自底而上形成结论、核心主张和全文结构。共同工作顺序为“明确目标成稿与写法→对照现状→落实动作→回查目标”，具体到全文、章节、图表、段落和句间关系。

## 写作依据

综合以下四篇论文的论证组织与表达方式，迁移其写作决策，不复制特色句或将作者结论移入新研究：

- Li 与 Zhang：圆柱尾流的强化学习控制及稳定性分析，JFM 2022。
- Kochkov 等：Machine learning–accelerated computational fluid dynamics，PNAS 2021。
- Li 等：Fourier Neural Operator for Parametric Partial Differential Equations，ICLR 2021。
- Lu 等：Learning nonlinear operators via DeepONet based on the universal approximation theorem of operators，Nature Machine Intelligence 2021。

详细来源、DOI 和归档版本见 [sources.md](references/sources.md)。细读覆盖四篇正文的章节与论证安排，并逐句分析 19 个代表性自然段、128 个句子；不代表逐句穷尽全部全文。

## 安装与使用

在尚不存在同名目录时，将仓库克隆到 Codex 用户级 skills 目录：

```sh
git clone https://github.com/alanZee/academic-writing-prediction.git ~/.codex/skills/academic-writing-prediction
```

若使用自定义 Codex 用户目录，请将目标路径改为该目录下的 `skills/academic-writing-prediction`。已有同名安装时先核对其来源，勿覆盖未保存的本地修改。

调用示例：

```text
使用 $academic-writing-prediction，依据我提供的研究问题、方法和已有结果，
明确手稿应具备的主旨、论证、证据和表达，以及怎样写成。
按我指定的范围设计大纲、撰写正文，或审查、优化、重构已有稿件。
明确区分已有发现与待做实验，不编造数值或机制结论。
```

只润色一个段落时，可直接指定段落和修改目标；不要求启动整套研究规划。仅要求审查时输出有位置、依据和修改办法的意见；要求优化或重构时，将必要调整落实到指定稿件。写作请求不自动授权运行仿真、训练、投稿或上传其他研究材料。

## 文件导航

- [SKILL.md](SKILL.md)：入口、总纲、任务范围与按需加载。
- [论证流程](references/argument-architecture.md)：科学问题、实验判据、章节职责、段落与句间逻辑。
- [章节指南](references/sections.md)、[语言与风格](references/style.md)、[预测证据边界](references/prediction-evidence.md)、[原创示例](references/examples.md)。
- [来源及逐篇细读入口](references/sources.md)：版本对应与原文分析。
- [文献资源](assets/README.md)：JFM PDF、其余文献的原文链接及本地归档文件名；`agents/openai.yaml`：Codex 显示信息。

## 许可

本仓库的原创 skill 指令、分析文档、示例和配置采用 [MIT License](LICENSE)。使用、修改与再分发时保留版权声明和许可文本；许可完整条款以 `LICENSE` 为准。

MIT 许可不覆盖第三方论文 PDF、论文原文及其图表。第三方内容继续适用各自的版权与许可；随附 JFM PDF 采用 CC BY-NC-SA 4.0，详见 [文献资源说明](assets/README.md)。

## 文献归属与版本

文献作者、署名、图表及出版信息保留；目标文献不代表对本技能的背书。PDF 属于第三方文献，版权与许可沿用各自原文。本仓库随附 JFM 的 CC BY-NC-SA 4.0 版本，其余三份 PDF 可留作本地阅读副本，默认不纳入 Git；具体依据见 [文献资源](assets/README.md)。

分析采用 JFM 与 Kochkov 的作者预印本、FNO 的 arXiv v3、DeepONet 的五作者期刊排版版。JFM 副本不含私人阅读批注，正文和分页保持原版。阅读与引用时以来源表标注的具体版本为准。
