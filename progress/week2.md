# 第二周学习笔记：范文阅读与 LaTeX 基础

## 本周内容

接着第一周的计划，这一阶段主要做了范文阅读和基础排版练习。阅读时，把摘要中的一项任务拆成“问题、方法、结果、正文证据”四部分；排版使用本机 MacTeX，重点练习公式编号、图表引用和参考文献。

比起只看论文用了哪些模型，更需要弄清楚作者为什么写这个结果，以及读者能在哪里找到依据。

## 范文阅读：从摘要找到正文证据

阅读材料是 2023 MCM C 题、队号 2314151 的 *Breaking the Wordle*。本次记录集中在 Summary 中预测成绩报告数量的部分，以及正文 §4.1.4 的结果表。

| 阅读要点 | 整理后的记录 |
| --- | --- |
| 问题 | 预测 2023 年 3 月 1 日的 Wordle 成绩报告数量。 |
| 方法 | 使用基于 Prophet 的时间序列预测模型，考虑趋势、季节性和节假日影响。 |
| 结果 | 摘要给出的预测区间为 `[10355, 18742]`。 |
| 正文证据 | §4.1.4 Result，Table 6: Predicted results；PDF 第 10 页，纸面页码 9。 |

以上内容对应[范文摘要与 Table 6（第三方镜像 PDF）](https://reformship.github.io/pages/3competition/4mcm/MCM%20Outstanding/2023/C/2314151.pdf)。Table 6 列出了具体的预测值和上下界，摘要则用整数区间概括结果。

这次阅读要记住两点：预测对象是“成绩报告数量”；区间是模型给出的预测，不能直接写成实际观测结果。摘要里的关键数字，也应当能在正文找到。

## LaTeX 排版：让编号与引用对应起来

练习文件采用一个简单的匀速运动例子，数字只用于排版演示。源文件见 [main.tex](../practice/week2/main.tex)，文献条目见 [references.bib](../practice/week2/references.bib)。

在原有距离公式前插入速度公式后，距离公式的编号由 `(1)` 变成了 `(2)`，正文中的引用也随之更新。这个练习说明，正文应通过标签引用公式，而不是手写编号。

```latex
\begin{equation}
  s(t)=vt
  \label{eq:distance}
\end{equation}

Equation~\eqref{eq:distance}
Table~\ref{tab:distance}
Figure~\ref{fig:distance}
```

`\label` 为对象设置名称，`\eqref` 引用带括号的公式编号，`\ref` 引用图表等对象的编号。图表的 `\label` 放在 `\caption` 后面，让标签取得对应的编号。

图表练习中补充了两句说明：表中 10 秒对应 20 米，图中距离随时间线性增长。写正文时，除了提到图表编号，还需要解释它提供了什么信息。

## 参考文献：用文献键连接正文与条目

当前源码中已经加入了两处 `\citep{wordle2023}`。其中 `wordle2023` 是 `.bib` 文件中的文献键；PDF 中显示的 `[1]` 则由排版系统生成。同一篇文献可以在正文出现多次，文末共用一个条目。

在仓库根目录可用以下命令编译和打开 PDF：

```bash
latexmk -cd -xelatex -interaction=nonstopmode -halt-on-error -outdir=build practice/week2/main.tex
open practice/week2/build/main.pdf
```

`latexmk` 会按需运行 XeLaTeX 和 BibTeX，并处理交叉引用。源文件保存修改后，要打开本次编译输出的 PDF，避免误看旧版本。

