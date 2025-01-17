---
sidebar_position: 7
---

# 🟢 规范化提示

import FormalPrompt from '@site/docs/assets/basics/formal_prompt.svg';

<div style={{textAlign: 'center'}}>
  <FormalPrompt style={{width:"800px",height:"300px",verticalAlign:"top"}}/>
</div>

我们现在已经涵盖了多种类型的提示，以及如何组合它们的方法。本篇教程将为您提供术语来解释不同类型的提示。虽然已经有方法来形式化提示工程中的术语(@white2023prompt)，但这个领域正在不断变化，因此我们将为您提供更充足的信息以便开始。

## 提示的组成部分

以下是在一个提示中将时常看到的一些组成部分：

- 角色
- 指令/任务
- 问题
- 上下文
- 示例(few shot)

在之前的教程中，我们已经涵盖了角色、指令和示例。问题则是简单的单一问题！（例如，“法国的首都是什么？”）。上下文则是任何与你想要模型作出的回应有关的信息。

并不是每个提示都包含所有这些组成部分，并且当某些部分出现时，它们之间也没有标准的顺序。例如，以下两个提示，每个提示包含一个角色、一个说明和一个上下文，虽然描述顺序有差异，但是我们期望他们做的事情是一样的：

```text
你是一名医生。请阅读这份病史并预测患者的风险：

2000年1月1日：打篮球时右臂骨折。戴上石膏进行治疗。
2010年2月15日：被诊断为高血压。开了利辛普利的处方。
2015年9月10日：患上肺炎。用抗生素治疗并完全康复。
2022年3月1日：在一次车祸中患上脑震荡。被送进医院接受24小时的监护。
```

```text
2000年1月1日：打篮球时右臂骨折。戴上石膏进行治疗。
2010年2月15日：被诊断为高血压。开了利辛普利的处方。
2015年9月10日：患上肺炎。用抗生素治疗并完全康复。
2022年3月1日：在一次车祸中患上脑震荡。被送进医院接受24小时的监护。

你是一名医生。请阅读这份病史并预测患者的风险：
```

然而，第二个提示其实更好，原因是指令是提示的最后一部分，这时候语言模型将更倾向于按指令执行而不是进一步输出上下文相关的信息。例如，如果给定第一个提示，语言模型可能会回复：`2022年3月15日:与神经科医生预约随访，以评估脑震荡恢复进展`，而不是直接预测患者的风险。


## 一份 “标准的” 提示

到目前为止，我们已经了解了几种不同格式的提示。现在，我们将定义一个“标准的”提示是什么样子的。根据 Kojima 等人的说法（@kojima2022large），我们将仅由问题组成的提示称为“标准”提示，同时，仅由问题组成且以 QA 格式存在的提示也是“标准”提示。

#### 为什么我们需要关心?

在我们引用的许多文章/论文中都使用了这个术语。我们定义这个术语是为了与标准提示相比讨论新类型的提示。

### 两个标准提示的例子:


_标准提示_
```
法国首都是什么?
```

_QA 格式的标准提示_
```
Q: 法国首都是什么?

A:
```

## 多示例的标准提示

多示例的标准提示(@liu2021pretrain)只是在标准提示的基础上附带多个需要解决的任务的范例(@brown2020language)。在研究中，多示例的标准提示有时也会直接称为标准提示（虽然我们在本指南中尽量避免这样称呼）。

### 两个多示例标准提示的例子:

_多示例标准提示_

```
西班牙的首都是什么？
马德里
意大利的首都是什么？
罗马
法国的首都是什么？
```

_QA 格式的多示例标准提示_
```
Q：西班牙的首都是什么？
A：马德里
Q：意大利的首都是什么？
A：罗马
Q：法国的首都是什么？
A：
```

多示例提示有助于上下文学习，这意味着模型无需更新参数就能够进行学习输出(@zhao2021calibrate)。

By [gezilinll](https://github.com/gezilinll).