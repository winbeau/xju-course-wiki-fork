# 编译原理笔记

## 引论

1. 什么是编译程序：把一种语言（源语言）书写的程序翻译成另一种语言（目标语言）的等价程序。
1. 编译过程

```mermaid
graph LR
A[源程序] --> B[词法分析]
B --> C[语法分析]
C --> D[语义分析]
D --> E[中间代码生成]
E --> F[代码优化]
F --> G[目标代码生成]
G --> H[目标程序]
```

## 文法和语言

1. **文法**：四元组 $(V_N, V_T, P, S)$，其中 $V_N$ 为非终结符集合，$V_T$ 为终结符集合，$P$ 为产生式集合，$S$ 为开始符号。$V_N \cap V_T = \phi$，$V_N \cup V_T = V$，$V$ 为所有符号集合。
1. **规则**（重写规则、产生式、生成式）：是形如 $\alpha \rightarrow \beta$ 或 $\alpha ::= \beta$ 的 $(\alpha, \beta)$ 有序对，其中 $\alpha$ 为产生式左部，$\beta$ 为产生式右部。$\alpha \rightarrow \beta$ 或 $\alpha ::= \beta$ 读作 *定义为* 。
1. **直接推导**：设 $\alpha \to \beta$ 是文法 $G=(V_N, V_T, P, S)$ 的规则，$\gamma$ 和 $\delta$ 是 $V^*$ 中的任意符号，若有符号串 $v, w$ 满足$v = \gamma \alpha \delta,~w = \gamma \beta \delta$，即说 $v$ 直接产生 $w$，或说 $v$ 是 $w$ 的直接推导，或说 $w$ 直接归约到 $v$，记作 $v \Rightarrow w$。
1. **多步推导 $(\geq 1)$**：$v \xRightarrow{+} w$
1. **多步推导 $(\geq 0)$**：$v \xRightarrow{*} w$
1. **句型**：设 $G[S]$ 是一个文法，如果符号串 $x$ 是从识别符号推导出来的，即有 $S \Rightarrow x$，则称 $x$ 是文法 $G[S]$ 的句型。
1. **句子**：若 $x$ 仅由终结符号组成，即 $S \Rightarrow x, x \in V_T^*$，则称 $x$ 为 $G[S]$ 的句子。