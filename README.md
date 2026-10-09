# 题目迭代

用于 Excel 题目的持续迭代：保存模型真实答错的题目及必要上下文，形成 Base Excel，并在历史题目的待求结果上接入新的业务逻辑，通过实际评分检查错误复现与传播

## 工作流程

1. 完成符合项目要求的题面、任务 Excel、参考答案和评分规则，冻结版本后上传评分
2. 下载各模型真实答卷，保存有效历史错题、必要上下文和下一轮 Base Excel
3. 基于 Base Excel 增加有业务意义的依赖题目，验证参考答案并按冻结规则评分
4. 历史题目本轮答对时，检查题面、数据、计算结构和答案提示，恢复受到影响的必要上下文
5. 将新增有效错题纳入历史记录，保存下一轮 Base Excel 和完整轮次记录

## 文件入口

- [SKILL.md](SKILL.md)：完整执行规则
- [上下文保留方法](references/context-retention_260926_2052.md)：依赖关系、上下文快照和逐轮核验
- [Rubrics 写作规范](references/rubric-plain-language_260929_1617.md)：评分规则、来源说明和错误原因
- [轮次记录模板](assets/round-record-template_260929_1617.md)：每轮身份、错题、依赖链、测试结果与下一轮文件
- [调用配置](agents/openai.yaml)：显示名称、默认提示词和自动调用设置

## 安装与调用

将此仓库内容安装到 `~/.codex/skills/excel-question-iteration/`，确保 `SKILL.md` 位于该目录根层

在任务中使用 `$excel-question-iteration`，并提供当前项目目录或 Base Excel。技能已配置 `allow_implicit_invocation: true`，支持按任务内容自动匹配

## 配套要求

- `historical-difficulty-bank`：安装到同级技能目录，供出题前查询难点、每道新题完成后登记考点及评分后补录错误
- `talentsai-excel-series3-authoring`：执行 Excel 大师第三期任务时，安装到同级技能目录并结合该项目的出题规范使用
- 实際执行时需要当前项目的源文件、适用规则、评分平台访问权限和本轮操作授权

历史案例中的本地链接记录作者保存的项目证据位置。用于自己的项目时，按实际文件位置维护证据路径与 SHA-256
