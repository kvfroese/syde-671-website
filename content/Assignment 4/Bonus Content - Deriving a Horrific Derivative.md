


The error is

$$
\begin{align*}
e_i&= p_i'-p_i \\
&= \frac{1}{y_3}\begin{bmatrix}
y_1 \\ y_2
\end{bmatrix}-p_i
\end{align*}
$$

Taking the derivative

$$
\pdv{e_i}{\mathbf{P}}=\pdv{}{\mathbf{P}}\left( \frac{1}{y_3} \begin{bmatrix}
y_1 \\ y_2
\end{bmatrix} \cancel{ - p_i } \right)
$$

Splitting the vector into a single component, with index 1 for both $\mathbf{e}$ and $\mathbf{P}$

$$
\begin{align*}
\pdv{e_1}{P_1}&= \pdv{}{P_1}\left( \frac{1}{y_3}y_1 \right) \\
\end{align*}
$$

Knowing that $y=M\mathbf{P}$, we can separate each $y_i$ into a dot product–based component

$$
\begin{align*}
y_1&= m_{11}P_1 + m_{12}P_2 + m_{13}P_3 + m_{14} \\
y_2 &= m_{21}P_1+m_{22}P_2+m_{23}P_3 + m_{24} \\
y_3&= m_{31}P_1+m_{32}P_2+m_{33}P_3 + m_{34}
\end{align*}
$$

We can now take the derivative of the $y_1$ and $y_3$–based equation as

$$
\begin{align*}
\pdv{e_1}{P_1}&= \pdv{}{P_1}\left( \frac{1}{y_3}y_1 \right) \\
&= \frac{y_1' y_3-y_1y_3'}{y_3^2} \\
y_1'&= m_{11}, y_3'=m_{31}\\
\implies \pdv{e_1}{P_1}&= \frac{m_{11}y_3 + y_1m_{31}}{y_3^2}
\end{align*}
$$

Similarly for $e_2$ we get

$$
\begin{align*}
\pdv{e_2}{P_1}&= \pdv{}{P_1}\left( \frac{1}{y_3}y_2 \right) \\
\pdv{e_2}{P_1}&= \frac{m_{21}y_3 + y_2m_{31}}{y_3^2}
\end{align*}
$$

Similarly for $P_2$

$$
\begin{align*}
\pdv{e_1}{P_2}&= \pdv{}{P_2}\left( \frac{1}{y_3}y_1 \right) \\
\pdv{e_1}{P_2}&= \frac{m_{12}y_3 + y_1 m_{32}}{y_3^2}
\end{align*}
$$

The entire Jacobian has format

$$
J=\begin{bmatrix}
\pdv{e_1}{P_1} & \pdv{e_1}{P_2} & \pdv{e_1}{P_3} \\
\vdots & \vdots & \vdots \\
\pdv{e_m}{P_1} & \pdv{e_m}{P_2} & \pdv{e_m}{P_3}
\end{bmatrix}
$$

