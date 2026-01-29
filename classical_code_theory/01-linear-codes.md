---
export:
  - format: pdf
  - format: tex
---
# linear codes

:::{prf:definition}
:label: linear code
a code $c$ that encodes $k$ bits of information into an $n$-bit space is called *linear* if every possible string to be encoded can be represented as a $k$-dimensional binary vector $v$ and it is encoded by the operation $gv$, where $g$ is an $n \times k$ matrix with entries in $\mathbb{z}_2$, independent of $v$, called a *generator matrix*. the vectors that form $g$ are typically chosen as a basis for the subspace of codewords. thus, every operation is performed modulo two and every possible codeword is a linear combination of these basis vectors. [https://doi.org/10.48550/arxiv.quant-ph/9705052]
:::


:::{prf:theorem}
:label: dual matrix of a linear code
given an $[n, k]$ linear binary code $c$ with binary generator matrix $g \in m_{n \times k}$, there exists a matrix $p \in m_{(n - k)\times n}$ such that for any vector $s$, $g s \in c$ if and only if $p s = 0$. more generally, a vector $v \in \mathbb{f}^n_2$ is a codeword if and only if $pv = 0$.
:::

:::{prf:proof}
:label: proof dual matrix of a linear code
by definition, a linear code $c$ is a $k$-dimensional subspace of $\mathbb{f}^n_2$. therefore, we can consider its orthogonal complement $c^\perp \subseteq \mathbb{f}^n_2$, defined as
$$c^\perp = \left\{w \in \mathbb{f}^n_2 \mid \forall v \in c, \langle w, v \rangle = 0\right\}.$$
it is known that the orthogonal complement has dimension $\dim(c^\perp) = \dim(\mathbb{f}^n_2) - \dim(c) = n - k$, so $c^\perp$ has a basis $\{p_1, p_2, \ldots, p_{n - k} \}$. we can then construct the matrix
$$p = \begin{pmatrix}p_1 \\ p_2 \\ \vdots \\ p_{n - k} \end{pmatrix}.$$

* ($\implies$) let $v \in c$. by the definition of $c^\perp$, we know that for each row $p_i$, $p_i v = 0$, and therefore $pv = 0$.
* ($\impliedby$) let $v \in \mathbb{f}^n_2$ such that $p v = 0$. this means that for every row $p_i \in p$, $p_i \cdot v = 0$, implying that $v \in (c^\perp)^\perp$. by {prf:ref}`complement of orthogonal complement`, we conclude that $v \in c$.
:::

:::{prf:lemma}
:label: complement of orthogonal complement
given a subspace $c \subseteq \mathbb{f}^n_2$ and its orthogonal complement $c^\perp$,
$$(c^\perp)^\perp = c.$$

by the definition of $c^\perp$, we know that $\forall v \in c$, $v \in (c^\perp)^\perp$. moreover, by calculating dimensions, we observe that
$$\dim((c^\perp)^\perp) = \dim(\mathbb{f}^n_2) - \dim(c^\perp) = n - (n - \dim(c)) = \dim(c).$$
since $c \subseteq (c^\perp)^\perp$ and both have the same dimension, they are the same subspace.
:::

:::{prf:example}
:label: first example linear code
for example, the repetition code can be thought of as a linear code with generator matrix
$$g = \begin{bmatrix}1 \\ 1 \\ 1\end{bmatrix}.$$
it then receives any single bit of information (represented in this case as a vector, as noted earlier), producing:
$$\begin{bmatrix}1 \\ 1 \\ 1\end{bmatrix} \begin{bmatrix} 0 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \\ 0 \end{bmatrix};\quad \begin{bmatrix}1 \\ 1 \\ 1\end{bmatrix} \begin{bmatrix} 1 \end{bmatrix} = \begin{bmatrix} 1 \\ 1 \\ 1 \end{bmatrix}.$$

we can define the parity matrix as
$$p = \begin{bmatrix}1 & 1 & 0 \\ 1 & 0 & 1\end{bmatrix}.$$

errors can be checked as follows:
* if $p s = (0, 0)$, there was no error.
* if $p s = (1, 0)$, the error occurred in the second bit.
* if $p s = (0, 1)$, the error occurred in the third bit.
* if $p s = (1, 1)$, the error occurred in the first bit.
:::
