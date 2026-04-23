# Kurdyka–Łojasiewicz 与 Mirror Descent 收敛（笔记导出版）

> 与 [`.cursor/skills/kurdyka_lojasiewicz_convergence/SKILL.md`](../.cursor/skills/kurdyka_lojasiewicz_convergence/SKILL.md) 同步；**数学以本仓 BGW 论文** [mainbody.tex](../BGW_sustech_ShenBohan/sections/mainbody.tex) / [appendices.tex](../BGW_sustech_ShenBohan/sections/appendices.tex) **为准**；**与算法弱耦**的**逐步全证明**（与教材 (4.4)–(4.6)、定理 30/31 同型）以 Skill **§5.8** 为准；本节为要点提纲。

## 1. 记号

- 文中「**KL 性质**」= **Kurdyka–Łojasiewicz**；**不与** 负熵 / **Kullback–Leibler 散度**、\(D*{KL}\)、\(D*\phi\) 混用简称而不加说明。
- KŁ 的**可积**形式在 BGW 中写为：存在去奇异化 \(\varphi\)，在邻域与值间隙内
  \[
  \varphi'\bigl(f(x)-f(\bar x)\bigr)\,\operatorname{dist}\bigl(0,\partial f(x)\bigr) \ge 1.
  \]
  **光滑** 内点无约束时 \(\operatorname{dist}(0,\partial f)=\lVert\nabla f\rVert\)。

## 2. 与算法弱耦的 KŁ 全链（教材范式，要点）

1. **充分下降** + **相对误差** \(\operatorname{dist}(0,\partial F(x_k)) \le c\lVert x_k - y_k\rVert\)（由 prox 一阶性构造 \(u_k\in\partial F(x_k)\)）。
2. **均匀 KŁ**：\(\varphi'(r_k)\,\operatorname{dist} \ge 1\)，与 (1) 合并得 \(\varphi'(r_k)\) 对 \(\lVert x_k-y_k\rVert\) 的下界。
3. **\(\varphi\) 凹且可导**：\(\varphi(b) \le \varphi(a) + \varphi'(a)(b-a)\)，取 \(a=r*k\)、\(b=r*{k+1}\)，用充分下降把 \(F(x*k)-F(x*{k+1})\) 换成步长平方项，得 \(\varphi(r*k)-\varphi(r*{k+1})\) 与步长的**差分不等式**（Skill §5.3 提纲，§5.8 全式）。
4. **AM–GM**：对 \(\sqrt{AB}\) 用 \(2\sqrt{AB}\le A+B\)，**拆开**乘积、配 **望远镜** \(\Psi*k-\Psi*{k+1}\) 与 \(\sum_k\lVert x_k-y_k\rVert\)（Skill §5.4；与联合目标附录 **Step 2** 同型；逐步见 §5.8）。
5. **求和** \(\Rightarrow\) 有限长 \(\Rightarrow\) Cauchy \(\Rightarrow\) 全序列收敛；**幂型** \(\varphi(s)=\tfrac{C}{\theta}s^\theta\) 时按 **\(\theta\)** 得有限终止/几何/次线性等**率**（教材定理 30–31 型，Skill §5.6 提纲与 §5.8 末段）。

## 3. BSTV18（Appendix 6, Thm 6.2）骨架

在 **Bolte–Sabach–Teboulle–Vaisbourd (2018)** 的抽象框架中，有界下降序列若满足 **(C1)(C2)(C3)** 且 **KŁ / uniformized KŁ**，则
\[
\sum_k \lVert x^{k+1}-x^k\rVert < \infty.
\]
证中常**打包** 3–4 步，**不** 逐行展开凹性与 AM–GM；与第 2 节**同精神**。

## 4. BGW 内层 MD 的要点（与附录逐式对应）

- **(C1)**：\(\varepsilon>L\) 得充分下降，再用 Pinsker 等将 Bregman 项下界到 **\(\lVert\pi^{t+1}-\pi^t\rVert_F^2\)**，得 (eq:bstv-c1) 型。
- **(C2)**：由子问题一阶性定义 **\(w^{t+1}\)**（(eq:bstv-w)），在截断域 **\(\tilde{\mathcal C}\_\tau\)** 上 **\(\nabla\phi=\log\pi+\mathbf 1\)** **整体 Lipschitz**（\(\pi\_{ik}\ge\tau\)），得 **(eq:bstv-c2)**。
- **KŁ**：\(G\_{D',\tau}\) 为 subanalytic \(\Rightarrow\) 在临界点处 KŁ；再据 BSTV18 Lemma 6.2 作 **uniformized** 邻域。
- **结论**：(eq:summable) **\(\sum_t\lVert\pi^{t+1}-\pi^t\rVert_F<\infty\)**。

## 5. 唯一极限与临界点（与原文一致）

- **\(\sum\lVert\cdot\rVert<\infty\)** 在**完备**赋范空间 \(\Rightarrow\) **Cauchy** \(\Rightarrow\) **唯一**极限 \(\pi^\ast\)。
- **\(0\in\partial G(\pi^\ast)\)**：\(w^{t+1}\to 0\)，**且** **\(G(\pi^t)\to G(\pi^\ast)\)**，用 **Rockafellar–Wets, Prop. 8.7** 的**闭**性。

## 6. 联合交替

- 联合目标见 BGW §[联合]；(H1)–(H3) + KL 路线对应 **BST14** PALM，细节在附录 `app:joint`。
- **Step 2（AM–GM 消去步长比）** 即第 2 节第 4 步的**同型**技巧；**内层** (C1)–(C2)+KŁ **不依赖** 该步。

## 7. 与凸证明的差异（一句话）

- 凸/强凸：常用**全局**一阶/强凸不等式直接**收缩**到最优点。
- KŁ 线：**(C1)(C2)** + **KŁ** + **\(\varphi\)** 的**凹**一阶界 + 必要时 **AM–GM** \(\Rightarrow\) 可和步长与**率**；**闭性**保证极限**临界**。

---

**最后同步**：改本文时请对照更新同目录上级的 **Skill** 文件。
