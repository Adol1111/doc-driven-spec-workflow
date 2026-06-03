# Practical Skill Writing

这份文档不讨论兼容性，只回答一件事:

基于 [WORKFLOW-STRUCTURE.md](/Users/gaoxiaoyi/projects/skills/doc-driven-spec-workflow/WORKFLOW-STRUCTURE.md)，这套 workflow 的 skills 从实用角度到底应该怎么写。

目标不是保留历史 prompt 习惯，而是让一个新 agent 在新对话里也能稳定恢复阶段、做对当前动作、在正确停点停下。

## 一句话结论

这套 skills 应该写成:

1. 一个极薄的 root router skill
2. 四个真正干活的 stage skills
3. 一个执行阶段 skill
4. 少量 reference/template 文件

也就是:

- `doc-driven-spec-workflow`
- `docs-workflow-bootstrap`
- `planning-clarification`
- `milestone-planning`
- `task-preparation`
- `task-execution-simple`

`task-spec-execution` 这种兼容层从实用角度不该存在。

## 先定原则

如果完全忘掉当前已有 skills，按 `WORKFLOW-STRUCTURE.md` 倒推，真正稳定的原则只有这些。

### 1. 文档是状态，不是聊天记忆

skill 的首要职责不是“把流程解释清楚”，而是“告诉 agent 去哪里找当前状态”。

所以每个会路由的 skill 都只该强调:

- 先看哪些 docs
- 这些 docs 各自是否 authoritative
- 缺失代表什么信号
- 当前 prompt 只作为最后一层补充证据

### 2. root 只负责选 stage

root skill 不该承担任何模板、编辑、落盘、评审、提交、实现细节。

它只回答:

- 现在处在哪个 stage
- 为什么是这个 stage
- 下一步交给哪个 skill
- 当前停点是 review pause 还是 hard gate

如果 root 写太厚，后面每个 stage skill 都会和它重复，最终 prompt 既长又容易冲突。

### 3. stage 边界要按“决策类型”切，不按文档类型切

最容易写坏的方式是:

- bootstrap 管创建文件
- planning 管写 roadmap 文件
- preparation 管写 spec 文件

这只是“写什么文件”的视角，不是“解决什么决策”的视角。

实用写法应该是:

- `bootstrap`: 解决“最小 scaffold 是否存在”
- `planning-clarification`: 解决“目标和边界是否明确”
- `milestone-planning`: 解决“交付结构怎么拆”
- `task-preparation`: 解决“当前任务是否已经清晰到可以开始实现”
- `task-execution-simple`: 解决“如何在隔离环境中完成一个已准备好的任务并收尾”

文档只是这些决策的落点。

### 4. review pause 和 hard gate 必须是全 workflow 的统一语义

这是整个结构里最值得保留的部分。

每个 skill 都不该重新发明自己的停点语义，而应该共享统一约定:

- `review pause`: 可以自然恢复，不额外引入审批门
- `operational step`: agent 可以顺着做
- `hard gate`: 必须显式确认

这比大量“如果用户说 continue 就怎样”的零散规则更重要。

### 5. 每个 stage skill 只拥有一个 stop model

实用上最怕 skill 同时负责:

- 写内容
- 评审
- 提交
- 交接
- 下一阶段的一部分工作

所以应该强制每个 skill 只拥有一种完整的工作闭环:

- 输入前提
- 核心动作
- 产出
- 默认停点
- 默认后续

这样 fresh conversation 才好恢复。

## 推荐的 skill 架构

## A. `doc-driven-spec-workflow`

### 它应该很薄

它只保留 4 块:

1. 证据顺序
2. stage 选择条件
3. handoff 输出格式
4. 什么时候必须问一个最小路由问题

### 它应该包含什么

- `Use when`: 用户要继续 docs-driven 工作，但下一步 stage 还没显式固定
- `Evidence order`: 直接引用 `WORKFLOW-STRUCTURE.md` 里的顺序
- `Routing table`: scaffold / ambiguity / roadmap shape / task readiness
- `Output contract`:
  - `Current stage`
  - `Why`
  - `Decided`
  - `Undecided`
  - `Next skill`
  - `Stop point`
- `Boundary rule`: root 只决定应该进入哪个 stage，不替 stage skill 提前做内部判断

### 它不该包含什么

- 具体模板路径
- 具体 spec/plan 写法
- 分支策略
- 提交策略
- 大量 edge case 文案
- 对某个 stage 的局部产出作主张，例如替 `task-preparation` 决定 spec 细节，或替 `task-execution-simple` 决定 closing outcome

### 实用写法建议

root skill 只要 60 到 100 行左右。能用表格的地方就用表格，不要长篇 prose。

## B. `docs-workflow-bootstrap`

### 它的唯一目标

补齐最小入口文档，让后续 skill 有状态可读。

### 它应该拥有的内容

- 最小 scaffold 的精确定义
- 创建哪些文件
- 每个文件只写什么最小内容
- 明确说不能创建 milestone/task/spec/plan
- bootstrap 完成后的默认停点是 review pause

### 它的核心判断

不是“用户想不想规划”，而是“后续阶段是否已经有最小状态承载体”。

### 它的输出

- 创建或更新了哪些 scaffold 文件
- 还没有解决的方向性问题
- 推荐下一 skill: `planning-clarification` 或 `milestone-planning`

### 它不该拥有

- roadmap 分解
- 把用户大段需求直接摊平成 tasks
- 任何 implementation spec

## C. `planning-clarification`

### 它的唯一目标

消除会影响 roadmap 结构的目标歧义。

### 它应该怎么写

这个 skill 不该围绕“写文档”组织，而应该围绕“提出阻塞性问题”组织。

它应该明确:

- 什么算 blocking ambiguity
- 一次只问一个问题
- 每个问题要给推荐答案
- 如果 docs 能回答，先读 docs，不先问人
- 输出是澄清结论，不是 roadmap
- 它处理的是 roadmap-blocking ambiguity，不是开放式 product discovery

### 它应产出的内容

- 更新 `planning-inbox` 或相关 planning docs
- 列出已经明确的目标、边界、当前不做什么
- 说明现在是否已经能进入 `milestone-planning`

### 它不该拥有

- 正式 milestone/task 分解
- spec 草拟
- “顺手先做一个可行 task”

### 实用提醒

这是最容易失控变成长咨询 prompt 的 skill。应该把它压成“只处理阻塞 roadmap 的歧义”，否则会吃掉整个流程。
如果问题已经从“目标不清”变成“怎么拆交付结构”，就应该停止追问，交给 `milestone-planning`。

## D. `milestone-planning`

### 它的唯一目标

把已经足够明确的方向，拆成可管理的 roadmap 结构。

### 它应该拥有的内容

- milestone 边界怎么定
- module 什么时候需要
- task 怎么按 capability outcome 切
- `Roadmap confirmed` 的含义
- handoff notes / planning inbox / backlog / completed milestone 的治理
- planning review pause

### 它最重要的规则

这个 skill 只拥有 docs governance，不拥有 task-local design。

所以它创建的 task 文档只该回答:

- 任务是什么
- 在哪里
- 顺序和依赖是什么
- 验收点大概是什么

但不该回答:

- 具体怎么改代码
- 测试顺序
- rollout 细节
- implementation slices

这些要留给 `task-preparation`。
task 粒度还要再加一条硬约束: 一个 task 应该对应一个可单独 review、单独交接、单独完成的 capability outcome，而不是一个笼统阶段名。

### 它应该怎么输出

- 推荐 milestone 结构
- 是否需要 modules
- 每个 milestone 下的 tasks
- 为什么这么拆
- 哪些地方仍未确认
- 默认停在 planning review pause

### 它不该拥有

- spec.md
- plan.md
- 执行分支
- readiness
- code edits

### 它何时应该停下或回退

- 如果 roadmap 结构仍依赖未解决的目标分歧，回到 `planning-clarification`
- 如果用户要求开始实现，但当前 milestone 仍未确认，只能停在 planning review 或询问是否继续做 provisional decomposition
- 如果 task 只能靠 implementation slices 才拆得开，说明 task 边界还不对，继续重构 roadmap，而不是把设计细节塞进 planning

## E. `task-preparation`

### 它的唯一目标

把一个已选中的 concrete task，收敛到“可以实现”的状态。

### 它才是 spec skill

如果从实用角度重写，这个 skill 应该非常聚焦:

1. 检查 task 是否真的 selectable
2. 先跑 clarification loop
3. 一次性写出 `spec.md`
4. 必要时再写 `plan.md`
5. 在 review 后做默认 follow-up
6. 交接给 execution

### 它应该明确写死的内容

- selectable 的前提条件
- 什么问题算 blocking
- 什么情况下必须有 `plan.md`
- `plan.md` 只补实现顺序，不重复 spec
- 默认 review 通过后提交 docs，除非用户显式拒绝
- 什么时候必须停止写 spec 并回退到 `milestone-planning`

### 为什么这个 skill 要写得比现在更“窄”

因为它的目标不是“把任务想得尽量完整”，而是“只补足实现前必须知道的那些东西”。

实用上，这意味着它要压制两种冲动:

- 不要回头改 roadmap 结构
- 不要提前进入 execution readiness

一旦发现下面这些情况，默认不是继续补 spec，而是回退到 `milestone-planning`:

- 同一个 task 需要两个 mutually exclusive scope choices 才能成立
- 同一个 task 看起来需要两份 spec 才写得清
- acceptance 其实对应两个可以独立上线或独立 review 的 capability
- 关键依赖缺失到已经不是 task-local clarification，而是 roadmap sequencing 问题

### 它的推荐输出骨架

- `Task`
- `Readiness check`
- `Blocking questions`
- `Spec result`
- `Plan needed? why?`
- `Review stop`
- `Auto follow-up result`
- `Execution handoff`

### 它不该拥有

- branch/worktree 决策
- 代码修改
- 测试修复策略
- branch closing

## F. `task-execution-simple`

### 它的唯一目标

在不重新做 planning 的前提下，把一个准备好的任务完整做完并停在正确收尾点。

### 它应该拥有的内容

- 默认 branch isolation
- worktree 什么时候才值得用
- readiness checkpoint
- implementation
- verification
- docs/status updates after code changes
- implementation review pause
- branch closing hard gate

### 它应该怎么写

这个 skill 的重点不是“如何编码”，而是“如何把一个任务执行闭环做完整”。

所以它最该强调的是顺序:

1. 先隔离
2. 再 readiness
3. 再实现
4. 再验证
5. 再更新 docs/status
6. 再 review
7. 最后进入 closing choice

### 它不该拥有

- 重新解释 spec
- 重新拆 task
- 因为实现困难就直接修改 roadmap

如果 execution 过程中发现 task 边界错了，应该显式回退到 planning，而不是在 execution skill 里偷偷重写任务定义。
execution 可以发现 spec 缺口，但默认只能做三件事: 提一个阻塞问题、记录发现、或建议回退；不能自己扩大 scope。

## 每个 skill 的统一模板

从实用角度，所有 stage skill 的 `SKILL.md` 都建议共用同一个基础骨架，但不要强迫所有 skill 长成完全一样。

推荐做法是:

- 一套通用骨架，保证 handoff 和边界一致
- 一些可选段落，只给真正需要的 stage 使用

这样可以避免 root 和 bootstrap 被写成和 execution 一样重。

```md
---
name: <skill-name>
description: <what it does>. Use when <clear trigger>.
---

# <Skill Title>

## Purpose
- One-sentence mission

## Use when
- ...

## Read first
- authoritative docs
- supporting docs
- current prompt

## Owns
- ...

## Must not own
- ...

## Entry checks
- only include when this stage has hard prerequisites

## Default flow
1. ...
2. ...
3. ...

## Stop point
- review pause | hard gate | handoff

## If blocked
- ask one question
- route back to previous stage
- stop for review

## Handoff
- Decided
- Undecided
- Next skill
- Stop point

## Optional sections
- `Do not use when`
- `Output`
- `Fixed prompt`
- `References`
```

这个模板比现在那种“quick start + mandatory rules + advanced features”更实用，原因是:

- 更像执行协议
- 更容易扫读
- 每个 section 的职责单一
- fresh agent 更容易恢复动作顺序
- 允许不同 stage 只保留自己真正需要的段落，不必机械对称

`Mandatory rules` 不是不能保留，但应该尽量吸收到 `Owns / Must not own / Entry checks / Default flow / If blocked` 里，而不是保留成一大段混合规则池。

## 旧版 skills 为什么会失效

如果回看旧版 skills，最典型的问题不是“少写了一条规则”，而是规则类型混在一起了，导致 agent 很难稳定判断:

- 什么时候只是 review pause
- 什么时候应该做默认收尾
- 什么时候已经可以进入下一阶段
- 什么时候必须停下来等 hard gate

### 问题 1: 说了 `continue / ok / go` 就直接进入下一阶段，没有先做本阶段收尾

这说明旧版 skill 没有把“阶段完成”写成闭环，而是把它写成一种模糊状态。

常见后果是:

- spec review 之后没有默认 commit reviewed docs
- implementation review 之后没有先 commit verified changes
- 进入下一阶段前没有更新 task status 或 handoff outcome
- branch closing 还没 resolved，就开始想着下一个 task
- merge / delete branch 前缺少显式确认链路

实用上要把这个问题写死成协议，而不是写成建议。

错误写法像:

- review 过后通常可以继续
- 之后一般会先 commit
- 然后进入下一阶段

更稳的写法应该像:

- `Review pause`: 先展示当前产出，等待用户 review
- `Default follow-up`: 用户用 `continue / ok / go` 表达前进意图后，先完成本阶段默认收尾
- `Stage transition`: 只有默认收尾完成后，才允许进入下一阶段

也就是说，`continue` 不应该直接等于 `go to next stage`，而应该等于:

1. 接受当前 review 结果
2. 触发默认 follow-up
3. follow-up 完成后再 handoff

对于不同阶段，这个默认 follow-up 要写清楚:

- `task-preparation`: commit reviewed task-local docs，除非用户显式要求先不 commit
- `milestone-planning`: 保留或提交 planning docs，并明确 handoff context
- `task-execution-simple`: commit verified implementation work，然后停在 implementation review 或 branch closing

而 destructive closing 永远不能被 `continue` 吞掉:

- `continue` 可以进入 closing choice
- 不能直接代表 `merge and delete branch`
- 更不能直接代表 `discard work`

### 问题 2: 不写禁止它就会主动做，不写建议它就可能完全不做

这说明旧版 skill 大量使用了模糊的语气词，但没有把规则分层。

模型最容易失控的情况就是:

- `should`
- `prefer`
- `typically`
- `if appropriate`

这些词单独看没错，但一旦缺少更强的协议语句，模型就会自己补全。

所以新 skill 最好把行为语句分成 4 类，并且显式写出来:

### 1. `Must`

不做就不能进入下一步。

例如:

- `Must not start another task while branch closing is unresolved.`
- `Must run the stage's default follow-up before handoff.`

### 2. `Default`

用户没有显式反对时，就这样做。

例如:

- `Default: after the final task-local review, commit reviewed docs before execution handoff unless the user explicitly asks to keep them uncommitted.`
- `Default: implement on a dedicated task branch, not the current branch.`

### 3. `Must not`

明确禁止模型靠自由发挥越界。

例如:

- `Must not let root choose task-local spec details.`
- `Must not let execution rewrite roadmap structure.`

### 4. `Exception`

只有满足明确定义的条件，才能偏离默认。

例如:

- `Exception: reviewed docs may remain uncommitted only when the user explicitly asks for that state.`
- `Exception: stay on the current branch only when the user explicitly chooses that path and the risk is surfaced.`

一句话总结就是:

- 不要把关键行为写成建议
- 不要把默认动作写成模糊倾向
- 不要让 hard gate 和 routine follow-up 混在一起

## 新版 skill 应该如何编码默认收尾

每个 stage 都应该有一个明确的 `review -> default follow-up -> handoff` 结构。

推荐写法:

### 1. 明确 review stop

例如:

- `Stop point: review pause after spec.md`
- `Stop point: implementation review after verified code changes`

### 2. 明确 review 后的默认动作

例如:

- `Default follow-up after approval: commit reviewed docs`
- `Default follow-up after approval: prepare execution handoff`
- `Default follow-up after implementation review: enter branch-closing choice`

### 3. 明确什么时候才算阶段结束

例如:

- `The stage is not complete until the default follow-up is resolved.`
- `Review approval alone does not skip the stage's routine closing actions.`

### 4. 明确什么是 hard gate

例如:

- `Deleting a branch always requires explicit confirmation at execution time.`
- `Discarding work always requires a fresh explicit confirmation for the current task.`

如果 skill 没把这四层写清楚，模型几乎一定会把“继续”理解成“直接往后跳”。

## 不要把所有严格规则都写成 hard gate

另一个常见失败模式是: 一旦把规则写严格，模型就开始要求用户给出特定审批措辞，例如 `我同意`、`我批准`、`我认可`，否则连 routine follow-up 都不执行。

这同样是不对的。

问题不在于规则太严格，而在于没有把下面两类信号分开:

- review pause 之后的前进信号
- hard gate 的动作确认

### review pause 之后需要的是 forward-motion，不是固定审批话术

对于 routine continuation，skill 应该接受任何清晰的前进表达，例如:

- `ok`
- `继续`
- `next`
- `go on`
- `往下`
- `可以`

这些表达已经足够说明用户要 agent 继续执行本阶段的默认后续动作。

所以更好的写法应该是:

- `Treat any clear forward-motion message as approval to perform the stage's default follow-up after a review pause.`
- `Do not require specific approval wording for routine operational steps.`

### hard gate 确认的是动作，不是某种固定句式

只有 destructive 或 high-risk action，才需要显式确认。

而且确认的重点应该是:

- 用户是否明确选择了这个动作

而不是:

- 用户有没有说出某个固定词

例如这些可以算有效 hard-gate 确认:

- `删掉这个分支吧`
- `选 2`
- `merge 之后删除`
- `就丢弃这次改动`

重点在动作意图明确，而不在形式统一。

### commit 往往是 default follow-up，不该被抬成 hard gate

在很多 stage 里，`commit` 本来就是 review 之后的常规收尾，而不是需要额外审批的危险动作。

例如:

- reviewed task-local docs commit
- verified implementation commit
- planning docs commit

除非当前上下文另有风险，或者用户明确要求保持 uncommitted 状态，否则这些都更适合编码成 `Default`，而不是 `Hard gate`。

一句话规则:

- `ok / continue / 继续 / next` 足以触发 routine follow-up
- 但不足以自动选择 destructive closing outcome

这样才能同时避免两种极端:

- 太松: 用户一说 `继续` 就直接跳阶段
- 太紧: 用户不说 `我批准` 就连 commit 都不做

## reference 文件应该怎么用

如果不考虑兼容性，reference 也应该收缩。

只保留三类:

1. 模板类
2. 固定问句类
3. 少数复杂 edge case 补充规则

具体建议:

- `bootstrap`: 一个 scaffold template
- `milestone-planning`: 一个 roadmap template
- `task-preparation`: 一个 spec template，一个 plan template
- `task-execution-simple`: 一个 branch-closing fixed prompt

不要把大量核心规则藏进 references 里。核心行为必须在 `SKILL.md` 主体可见。

reference 只适合放:

- 长模板
- 固定 wording
- 极少数不值得污染主 skill 的细节条款

## 这套 skills 真正该怎么拆写

如果现在从零重写，我建议按下面顺序进行。

### 第一步: 先重写 root

先把 `doc-driven-spec-workflow` 压薄，只留下路由协议。

如果 root 还厚，后面所有 stage skills 都会被它污染。

### 第二步: 重写 stage ownership

按上面的 A 到 F，先给每个 skill 写:

- `Use when`
- `Do not use when`
- `Owns`
- `Must not own`
- `Stop point`

先不要写细规则，先把边界写硬。

### 第三步: 再补 workflow steps

只有边界稳定后，再给每个 skill 补 4 到 8 条 workflow steps。

一上来就写大段 rules，通常会把边界问题掩盖掉。

### 第四步: 最后才抽 references

只有当某段内容:

- 明显过长
- 可复用
- 不属于主行为定义

再抽到 reference 里。

否则就留在 skill 主体。

## 建议的重写结果

如果完全按实用主义来收敛，最后每个 skill 大概应是这个量级:

- root: 60 到 100 行
- bootstrap: 80 到 120 行
- clarification: 80 到 140 行
- milestone-planning: 120 到 180 行
- task-preparation: 140 到 220 行
- task-execution-simple: 140 到 220 行

这已经足够大，但还在可维护范围内。

如果某个 skill 超出这个量级，通常说明:

- 边界没切干净
- 兼容性规则太多
- 把 edge case 当成主路径写进去了

## 最后给一个实用判断标准

一个 skill 写得对不对，不看它解释得多完整，而看它是否满足下面 5 条:

1. 新对话能不能只靠 docs 恢复当前 stage
2. agent 会不会把不属于本阶段的工作偷做掉
3. 用户说一句 `continue` 时，agent 会不会自然走到默认后续
4. destructive actions 会不会只出现在 hard gate
5. 下一阶段接手时，是否能只靠 handoff 四元组继续工作

如果这 5 条都满足，这套 skills 就已经实用了。

## 下一步建议

如果你认可这份拆法，下一轮最值得做的不是继续讨论原则，而是直接按这份文档重写:

1. `skills/doc-driven-spec-workflow/SKILL.md`
2. `skills/docs-workflow-bootstrap/SKILL.md`
3. `skills/planning-clarification/SKILL.md`
4. `skills/milestone-planning/SKILL.md`
5. `skills/task-preparation/SKILL.md`
6. `skills/task-execution-simple/SKILL.md`

重写时先删掉兼容层和历史措辞，再补最少量 references。
