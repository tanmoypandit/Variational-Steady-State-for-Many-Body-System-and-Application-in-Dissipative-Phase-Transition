\documentclass[11pt]{article}
\usepackage[margin=1in]{geometry}
\usepackage{amsmath, amssymb}
\usepackage{hyperref}
\usepackage{graphicx}

\title{Variational Steady State Simulation for Collective Dephasing}
\author{Tanmoy Pandit}
\date{}

\begin{document}

\maketitle

\section*{Overview}

This repository contains a QuTiP-based implementation of a variational algorithm for finding the non-equilibrium steady state (NESS) of a dissipative quantum system under collective dephasing. The approach is based on the McLachlan variational principle, which minimizes the trace norm $\mathrm{Tr}|\dot{\rho}|$ to approximate the stationary solution of the Lindblad master equation.

\section*{Methodology}

The variational ansatz used here is a product of single-qubit Bloch sphere states:
\[
\rho_i = \frac{1}{2} \left( \mathbb{I} + \vec{\alpha}_i \cdot \vec{\sigma} \right),
\]
and the full two-body state is taken as $\rho_{12} = \rho_1 \otimes \rho_2$.

We construct the effective Hamiltonian and Lindblad dissipators for a collective dephasing scenario:
\begin{itemize}
    \item Local Hamiltonian term: \( H_l = \frac{W}{2}(X_1 + X_2) \)
    \item Interaction term: \( H_{\text{int}} = \frac{V}{4} Z_1 Z_2 \)
    \item Mean-field effective term based on the variational state
\end{itemize}

The variational cost function is:
\[
\mathcal{C}(\vec{\alpha}) = \mathrm{Tr}|\dot{\rho}_{12}(\vec{\alpha})|
\]
which is minimized using the SLSQP algorithm from SciPy.

\section*{Output}

The notebook plots:
\begin{enumerate}
    \item Convergence of the cost function over optimization steps.
    \item Evolution of the six variational parameters.
\end{enumerate}

These results demonstrate convergence to the NESS under varying driving field strength \(W\).

\section*{Reference}

This variational steady-state technique builds upon the framework proposed in the following work:

\begin{itemize}
    \item H. Weimer, ``Variational Principle for Steady States of Dissipative Quantum Many-Body Systems,'' \textit{Phys. Rev. Lett.} \textbf{114}, 040402 (2015). \\
    DOI: \href{https://doi.org/10.1103/PhysRevLett.114.040402}{10.1103/PhysRevLett.114.040402}
\end{itemize}

\section*{Dependencies}

\begin{itemize}
    \item Python 3.7+
    \item \texttt{qutip}
    \item \texttt{scipy}
    \item \texttt{numpy}
    \item \texttt{matplotlib}
\end{itemize}

\end{document}
