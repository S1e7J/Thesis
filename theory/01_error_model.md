# Error Model

Creating a general mathematical model for error correction means that we should make as few assumptions as neccesary for the error (or noise) model that we will work with. That way if we define a method for solving this general errors it could be specialized into every other possible error. However, for simplicity we will still have some assumptions. For instance we will work in 2 dimentional hilbert space for every qubit (This is not required but it would simplify the examples and conclusion. However when neccesary the explanation of generalization would be provided) and we will make the broad assumption that the error is defined by an operation in that space. For this suppose we have a qubit in a state $\alpha_1 \ket{0} + \alpha_2 \ket{1}$ and an Error that is in the state $\ket{E}$. Then we would define the error as the operation


:::{prf:theorem}
:label: pauli is a base
The Set of Pauli operations $\mathcal{B} = \left\{I, Z, X,  ZX\right\}$ forms a base for the operations over a 2 dimentional Hilbert space.

_Proof:_

Given that the cardinality of $\mathcal{B}$ corresponde to the dimention of the operations over the Hilbert space it's sufficient to show that the set is linearly independent to show that it's a base. Therefore we can use the [Trace inner product](Trace Class Norm) that defines an inner product in matrixes $2 \times 2$.

\begin{align*}
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
\left<I, X\right> &=
Tr\left(
\begin{pmatrix}
1 & 0 \\
0 & 1
\end{pmatrix}^*
\begin{pmatrix}
0 & 1 \\
1 & 0
\end{pmatrix}
\right) =
Tr\left(\begin{pmatrix}
0 & 1 \\
1 & 0
\end{pmatrix}\right)\\
&= 0\\
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
\left<I, Z\right> &=
Tr\left(
\begin{pmatrix}
1 & 0 \\
0 & 1
\end{pmatrix}^*
\begin{pmatrix}
1 & 0 \\
0 & -1
\end{pmatrix}
\right) =
Tr\left(\begin{pmatrix}
1 & 0 \\
0 & -1
\end{pmatrix}\right)\\
&= 0\\
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
\left<X, I\right> &=
Tr\left(
\begin{pmatrix}
0 & 1 \\
1 & 0
\end{pmatrix}^*
\begin{pmatrix}
1 & 0 \\
0 & 1
\end{pmatrix}
\right) =
Tr\left(\begin{pmatrix}
0 & 1 \\
1 & 0
\end{pmatrix}\right)\\
&= 0\\
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
\left<X, Z\right> &=
Tr\left(
\begin{pmatrix}
0 & 1 \\
1 & 0
\end{pmatrix}^*
\begin{pmatrix}
1 & 0 \\
0 & -1
\end{pmatrix}
\right) =
Tr\left(\begin{pmatrix}
0 & -1 \\
1 & 0
\end{pmatrix}\right)\\
&= 0\\
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
\left<Z, I\right> &=
Tr\left(
\begin{pmatrix}
1 & 0 \\
0 & -1
\end{pmatrix}^*
\begin{pmatrix}
1 & 0 \\
0 & 1
\end{pmatrix}
\right) =
Tr\left(\begin{pmatrix}
1 & 0 \\
0 & -1
\end{pmatrix}\right)\\
&= 0\\
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
\left<Z, X\right> &=
Tr\left(
\begin{pmatrix}
1 & 0 \\
0 & -1
\end{pmatrix}^*
\begin{pmatrix}
0 & 1 \\
1 & 0
\end{pmatrix}
\right) =
Tr\left(\begin{pmatrix}
0 & 1 \\
-1 & 0
\end{pmatrix}\right)\\
&= 0\\
\end{align*}

Because of the theorem [](Theorem of Orthogonality to Lineality) we know that every unitary opertion in a Hilbert space can be represented by a linear combinations of the set $\mathcal{B}$
:::

:::{prf:definition}
:label:Trace Class Norm

For matrixes $n \times n$ you can define a Trace Class Norm as
$$\left<A, B\right> = Tr\left(A^*, B\right)$$

_Checks_:

We could first check that $\left<A, B\right> = \overline{\left<B, A\right>}$
\begin{align*}
\overline{\left<B, A\right>} &= \overline{Tr(B^*, A)}\\
&= Tr((B^*A)^*)\\
&= Tr(A^*B)\\
&= \left<A, B\right>
\end{align*}

\begin{align*}
\left<A, \alpha B + \beta C\right> &= Tr (A^*(\alpha B + \beta C))\\
&= Tr (\alpha A^* B + \beta A^* C)\\
&= \alpha Tr (A^* B) + \beta T (A^* C)\\
&= \alpha\left<A, B\right> + \beta \left<A, C\right>
\end{align*}

\begin{align*}
\left<A, A\right> &= Tr (A^*A)\\
&= \sum_{i = 1}^n (A^*A)_{ii}\\
&= \sum_{j = 1}^n\sum_{i = 1}^n \overline{a}_{ji} a_{ji}\\
\end{align*}

And we know that for ever complex value $\overline{a} a \geq 0$ therefore $\left<A, A\right> \geq 0$ also the only way to have $\overline{x}x = 0$ is with $x = 0$ and therefore $$\left<A, A\right> = 0 \implies A = 0$$
:::

:::{prf:theorem}
:label: Theorem of Orthogonality to Lineality
Given a set $\mathcal{B}$ of vectors without $0$ in vector space of dimention n and an inner product $\left<\cdot ,\cdot \right>$
$$\forall v_1, v_2 \in \mathcal{B}: v_1 \neq v_2 \left< v_1, v2 \right> = 0 \implies \mathcal{B} \text{ is linearly independent}$$

_Proof_

Let
$$\sum_{i = 0}^n a_i v_i = 0$$

We can now take a vector $v_k$ and take inner product of both sides

$$\left<v_k, \sum_{i = 0}^n a_i v_i\right> = \left<v_k, 0\right>$$

However, given that $\mathcal{B}$ is orthogonal $\forall i \neq k \implies \left<v_k, v_i\right> = 0$ and therefore every component would be remove except for
$$a_k \left<v_k, v_k\right> = 0 \implies a_k = 0$$ because $0 \notin \mathcal{B}$

We can repeat for every $k$ in the set and therefore $\forall k a_k = 0$ so $\mathcal{B}$ is linearly independent.
:::
