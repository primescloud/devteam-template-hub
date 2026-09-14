# <项目名>

这是一个 **devteam 项目的 hub 仓库**:人和 agent 在这里碰头。

它装文档、设计产出物和主线 issue,**不装产品代码**——代码住各自的 code 仓库,一个项目可以有好几个。

> 从模板 generate 出来后,把上面的标题和这一段换成这个项目自己的介绍。下面的内容是仓库约定,留着。

## 两个入口

找 agent 的方式只有两种,区别只在**这件事要不要进依赖图**:

| 你要做的 | 去哪 | 怎么结束 |
| --- | --- | --- |
| 派一件活——有明确范围和验收标准,会被 PR 关掉 | **Issues** → New issue | PR `closes #n` |
| 还没想清楚——质询、头脑风暴、待决的设计问题 | **Discussions** → New discussion → **Ideas** | 聊出结论 |

**任务轨没有表单**,直接开就行——仓库的协调者会读完再补规格、必要时追问。

**对话轨的表单有一个 `Agent` 下拉**,选你想找的角色。它不只是给人看的——**这一项就是路由依据**,
选谁就只有谁被叫醒。两个后果跟着来:

- **把帖子从别的 category 搬进 Ideas 是没用的。** 那种帖子正文里没有 `### Agent` 段,
  事件会被**丢弃**——没有人被叫醒,也不会有任何报错。要进对话轨就走 New discussion。
- **下拉里的名字必须是真实存在的角色 id**。填一个本项目没部署的角色,同样是静默丢弃。

两条规矩:

- **Discussions 不是第二个任务面。** 会被 PR 关掉的工作不放那儿,否则和 Issues 打架。
- **General 留给正常聊天**,对话轨只认 Ideas。

## generate 之后

模板给的是**种子**——仓库里的文件和分支结构,交付之后归这个项目自己演化,没人会再来改它。
label、topic、Discussions 开关、分支保护、看板是**投影**:由 `devteam project apply` 按项目声明写上去,
**人手改了下次 apply 会抹掉**。想改这些去改声明,别在 GitHub 界面上改。

还需要人做的:

1. 换掉本文件顶部的标题和介绍。
2. 把这个仓库接进项目声明,然后 `devteam project apply`。
3. Discussions 开关由 apply 负责,但 **Ideas category 是 GitHub 自带的**,开了就有,不用建。
4. **把 `ideas.yml` 里 `Agent` 下拉的 options 改成本项目实际部署的角色 id。** 模板只能给一个
   `leader` 占位——角色是项目级的,模板知道不了。漏了这一步,人就只能找 leader。
5. `.github/ISSUE_TEMPLATE/config.yml` 不在模板里——它要写死本仓库的 Discussions URL,
   模板给不出来。想在 New issue 页上挂一条「找 agent 聊聊」的引导,自己加。

**默认分支是 `develop`**,不是 `main`。generate 出来的仓库跟模板走,别改——整条交付链的最后一站是它。

## 仓库里有什么

| 路径 | 干什么的 |
| --- | --- |
| `AGENTS.md` | 给 agent 看的行为准则 + **文档地图**(什么东西该写在哪) |
| `docs/agents/*.md` | skill 的配置面:这个仓库的 issue tracker、label 词表、领域文档布局 |
| `.github/DISCUSSION_TEMPLATE/ideas.yml` | 对话轨入口。里面 `Agent` 下拉的 options **generate 之后要改成本项目实际的角色**，而 `label: Agent` 这个字符串是和路由器的约定，别改 |

**东西该写在哪以 `AGENTS.md` 的表为准**,这里不复制一份——两份就是两个真相。三条结论先摆在这:

- 版本要达成什么,写在 **GitHub milestone 的 description** 里,不写成文档;进度是 milestone
  自己算的计数,**任何文档都不记进度**。
- 调研笔记进 `docs/research/`,每条结论带出处。
- `CONTEXT.md` 和 `docs/adr/` 等到真有术语、真有决策时再建,**别先摆空架子**。

skill 本体不在这个仓库里——它跟着角色走,由 runner 装。仓库里只有上面那份**配置面**,
因为「这个仓库的 tracker 和 label 是什么」每个项目都可能不一样。
