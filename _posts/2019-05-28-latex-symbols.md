---
layout:   post
title:    "Latex 常用符号"
subtitle: "Latex symbols"
date:     2019-05-27
author:   "Eric"
catalog:  true
header-img: "img/post-bg-memory.jpg"
tags:
  - LaTeX
---

## 1. 字体
$$
\begin{array}{ll|l}
\texttt{"normal"}      &\texttt{}         & ABCDEFGHIJKLMNOPQRSTUVWXYZ \\ 
\texttt{"blackboard"}  &\texttt{\mathbb}  &\mathbb{ABCDEFGHIJKLMNOPQRSTUVWXYZ} \\ 
\texttt{"boldface"}    &\texttt{\mathbf}  &\mathbf{ABCDEFGHIJKLMNOPQRSTUVWXYZ}\\
\texttt{"typewriter"}  &\texttt{\mathtt}  &\mathtt{ABCDEFGHIJKLMNOPQRSTUVWXYZ}\\
\texttt{"roman"}       &\texttt{\mathrm}  &\mathrm{ABCDEFGHIJKLMNOPQRSTUVWXYZ}\\
\texttt{"sans-serif"}  &\texttt{\mathsf}  &\mathsf{ABCDEFGHIJKLMNOPQRSTUVWXYZ}\\
\texttt{"calligraphic"}&\texttt{\mathcal} &\mathcal{ABCDEFGHIJKLMNOPQRSTUVWXYZ}\\
\texttt{"script"}      &\texttt{\mathscr} &\mathscr{ABCDEFGHIJKLMNOPQRSTUVWXYZ}\\
\texttt{"fraktur"}     &\texttt{\mathfrak}&\mathfrak{ABCDEFGHIJKLMNOPQRSTUVWXYZ}\\
\end{array}
$$

## 2. 数学重音符号
$$
\begin{array}{ll|ll|ll}
\mathrm{\hat{a}} &\textbf{\hat{a}} 
&\mathrm{\check{a}} &\textbf{\check{a}} 
&\mathrm{\tilde{a}} &\textbf{\tilde{a}} \\ 
\mathrm{\grave{a}} &\textbf{\grave{a}} 
&\mathrm{\dot{a}} &\textbf{\dot{a}} 
&\mathrm{\ddot{a}} &\textbf{\ddot{a}} \\
\mathrm{\bar{a}} &\textbf{\bar{a}} 
&\mathrm{\vec{a}} &\textbf{\vec{a}} 
&\mathrm{\widehat{A}} &\textbf{\widehat{A}} \\
\mathrm{\acute{a}} &\textbf{\acute{a}} 
&\mathrm{\breve{a}} &\textbf{\breve{a}} 
&\mathrm{\widetilde{A}} &\textbf{\widetilde{A}} \\
\end{array}
$$

## 3. 希腊字母
$$
\begin{array}{llllllll}
\mathrm{\alpha} &\textbf{\alpha} 
&\mathrm{\theta} &\textbf{\theta} 
&\mathrm{o} &\textbf{o} 
&\mathrm{\upsilon} &\textbf{\upsilon} \\
\mathrm{\beta} &\textbf{\beta} 
&\mathrm{\vartheta} &\textbf{\vartheta} 
&\mathrm{\pi} &\textbf{\pi} 
&\mathrm{\phi} &\textbf{\phi} \\
\mathrm{\gamma} &\textbf{\gamma} 
&\mathrm{\iota} &\textbf{\iota} 
&\mathrm{\varpi} &\textbf{\varpi} 
&\mathrm{\varphi} &\textbf{\varphi} \\
\mathrm{\delta} &\textbf{\delta}
&\mathrm{\kappa} &\textbf{\kappa}
&\mathrm{\rho} &\textbf{\rho}
&\mathrm{\chi} &\textbf{\chi} \\
\mathrm{\epsilon} &\textbf{\epsilon}
&\mathrm{\lambda} &\textbf{\lambda}
&\mathrm{\varrho} &\textbf{\varrho}
&\mathrm{\psi} &\textbf{\psi} \\
\mathrm{\varepsilon} &\textbf{\varepsilon}
&\mathrm{\mu} &\textbf{\mu}
&\mathrm{\sigma} &\textbf{\sigma}
&\mathrm{\omega} &\textbf{\omega} \\
\mathrm{\zeta} &\textbf{\zeta}
&\mathrm{\nu} &\textbf{\nu}
&\mathrm{\varsigma} &\textbf{\varsigma} \\
\mathrm{\eta} &\textbf{\eta}
&\mathrm{\xi} &\textbf{\xi}
&\mathrm{\tau} &\textbf{\tau} \\
\mathrm{\Gamma} &\textbf{\Gamma}
&\mathrm{\Lambda} &\textbf{\Lambda}
&\mathrm{\Sigma} &\textbf{\Sigma}
&\mathrm{\Psi} &\textbf{\Psi} \\
\mathrm{\Delta} &\textbf{\Delta}
&\mathrm{\Xi} &\textbf{\Xi}
&\mathrm{\Upsilon} &\textbf{\Upsilon}
&\mathrm{\Omega} &\textbf{\Omega} \\
\mathrm{\Pi} &\textbf{\Theta}
&\mathrm{\Phi} &\textbf{\Phi}
\end{array}
$$

## 4. 二元关系符号
$$
\begin{array}{}
\mathrm{<} &\textbf{<}
&\mathrm{>} &\textbf{>}
&\mathrm{=} &\textbf{=} \\
\mathrm{\leq} &\textbf{\leq or \le}
&\mathrm{\geq} &\textbf{\geq or \ge}
&\mathrm{\equiv} &\textbf{\equiv} \\
\mathrm{\ll} &\textbf{\ll}
&\mathrm{\gg} &\textbf{\gg}
&\mathrm{\doteq} &\textbf{\doteq} \\
\mathrm{\prec} &\textbf{\prec}
&\mathrm{\succ} &\textbf{\succ}
&\mathrm{\sim} &\textbf{\sim} \\
\mathrm{\preceq} &\textbf{\preceq}
&\mathrm{\succeq} &\textbf{\succeq}
&\mathrm{\simeq} &\textbf{\simeq} \\
\mathrm{\subset} &\textbf{\subset}
&\mathrm{\supset} &\textbf{\supset}
&\mathrm{\approx} &\textbf{\approx} \\
\mathrm{\subseteq} &\textbf{\subseteq}
&\mathrm{\supseteq} &\textbf{\supseteq}
&\mathrm{\cong} &\textbf{\cong} \\
\mathrm{\sqsubset} &\textbf{\sqsubset}
&\mathrm{\sqsupset} &\textbf{\sqsupset}
&\mathrm{\Join} &\textbf{\Join} \\
\mathrm{\sqsubseteq} &\textbf{\sqsubseteq}
&\mathrm{\sqsupseteq} &\textbf{\sqsupseteq}
&\mathrm{\bowtie} &\textbf{\bowtie} \\
\mathrm{\in} &\textbf{\in}
&\mathrm{\ni} &\textbf{\in or \owns}
&\mathrm{\propto} &\textbf{\propto} \\
\mathrm{\vdash} &\textbf{\vdash}
&\mathrm{\dashv} &\textbf{\dashv}
&\mathrm{\models} &\textbf{\models} \\
\mathrm{\mid} &\textbf{\mid}
&\mathrm{\parallel} &\textbf{\parallel}
&\mathrm{\perp} &\textbf{\perp} \\
\mathrm{\smile} &\textbf{\smile}
&\mathrm{\frown} &\textbf{\frown}
&\mathrm{\asymp} &\textbf{\asymp} \\
\mathrm{:} &\textbf{:}
&\mathrm{\notin} &\textbf{\notin}
&\mathrm{\neq} &\textbf{\neq or \ne}
\end{array}
$$

## 5. 二元运算符号
$$
\begin{array}{}
\mathrm{+} &\textbf{+}
&\mathrm{-} &\textbf{-}
&\mathrm{\triangleleft} &\textbf{\triangleleft} \\
\mathrm{\pm} &\textbf{\pm}
&\mathrm{\mp} &\textbf{\mp}
&\mathrm{\triangleright} &\textbf{\triangleright} \\
\mathrm{\cdot} &\textbf{cdot}
&\mathrm{\setminus} &\textbf{\setminus}
&\mathrm{\star} &\textbf{\star} \\
\mathrm{\cup} &\textbf{\cup}
&\mathrm{\cap} &\textbf{\cap}
&\mathrm{\ast} &\textbf{\ast} \\
\mathrm{\sqcup} &\textbf{\sqcup}
&\mathrm{\sqcap} &\textbf{\sqcap}
&\mathrm{\circ} &\textbf{\circ} \\
\mathrm{\vee} &\textbf{\vee, \lor}
\end{array}
$$


